# Bounding box tool and entity detection 

```
Annotate this image in Python using Pillow (PIL) and execute it to output the annotated composite image.

=== 0. COORDINATE SYSTEM & CLAMPING ===
- Normalized coordinate space: 0 to 1000 on both axes. (0,0 = top-left, 1000,1000 = bottom-right).
- For EACH item, calculate:
  1) Center coordinates: (cx, cy) in range 0-1000.
  2) Width and Height: (w, h) in range 0-1000.
  3) Boundary clamping to prevent edge clipping:
     x0 = int(max(0, min(1000, cx - w/2)) * (image_width / 1000))
     y0 = int(max(0, min(1000, cy - h/2)) * (image_height / 1000))
     x1 = int(max(0, min(1000, cx + w/2)) * (image_width / 1000))
     y1 = int(max(0, min(1000, cy + h/2)) * (image_height / 1000))
- NEVER guess x0/y0/x1/y1 directly without center-first math.
- Pre-draw self-check: Confirm the item's center lands inside its physical boundaries and does not drift onto neighbors.

=== 1. VISUAL STYLE & PALETTE ===
- Photo Overlays: Clean outlines ONLY (2px stroke if width < 1200px, 3px if >= 1200px).
- Translucency & Fill: NONE. No tinted fills, no arrows, no floating text labels across the photo.
- Dot/Badge: Place a small solid circle (radius 10-12px) at (x0, y0) containing the numeric ID in contrasting text.
- Category Palette (Hex):
  - Red (#E53935): Furniture
  - Pink (#EC407A): Textile / Soft furnishing
  - Green (#43A047): Decor / Plants
  - Blue (#1E88E5): Architecture / Structure (use sparingly; see Rule 3)
  - Yellow (#FDD835): Small items / Electronics / Cables / Hardware
  - Cyan (#00ACC1): Outdoor / Background / Distant view
  - Orange (#FB8C00): Food / Drink / Offerings / Small containers
- Dimension Lines: Draw 1-2 clean baseline scale lines at the bottom of the photo with end ticks (e.g., "|--- SOFA ~210cm ---|").

=== 2. DRAW ORDER (Critical for Visual Hierarchy) ===
Draw sequentially to avoid burying smaller annotations:
  1) Largest background boxes (if qualified under Rule 3)
  2) Large furniture / architectural masses
  3) Medium items (bowls, crates, plates, pots)
  4) Small items LAST (diyas, switches, petals, hardware)
  * Rule: Never draw an enclosing container after the items nested inside it.

=== 3. WHAT TO BOX vs WHAT TO LIST ONLY ===
- DO NOT BOX surfaces covering >60% of the image (e.g., Wall, Floor, Ceiling, Sky, Carpet). Designate them as "[LIST ONLY]" in the legend, tree map, and telemetry.
- DO NOT BOX the full cloth or table if it spans >=80% of image width. Box ONLY if <80% width. Otherwise designate "[LIST ONLY]".
- DO BOX: Distinct furniture, appliances, individual cushions, plants, containers, food groupings, lamps/diyas, windows/doors (<80% width).
- MINIMUM BOUND RULE: If an object is <25px in either dimension in the native image, DO NOT draw a rectangle. Plot ONLY an 8px numbered center dot at (cx, cy) and list it.

=== 4. EXTRACTION HIERARCHY (Extract 20-30 Distinct Items) ===
Audit the image across these 11 tiers in order:
  1. Main furniture / altar / table: Name, shape, primary footprint.
  2. Cushions / textiles: Color, weave/pattern, placement.
  3. Containers: Bowls, crates, plates, pots, boxes (record contents).
  4. Food / consumables: Separate distinct items (do not lump dissimilar foods together).
  5. Flora: Plants, flowers, stems (group only if identical and contiguous).
  6. Light sources: State LIT / UNLIT, flame or glow visibility (Y/N).
  7. Architecture: Openings, trim, outlets, downlights (apply the 60% rule).
  8. Outdoor / background: Visible depth planes beyond apertures.
  9. People (if present): Stance, attire, occlusion status (1 box per person).
  10. Lighting environment: Natural vs artificial balance, shadow direction, timestamps.
  11. Condition & state: Fresh/wilted, active/static, tidy/disordered.

=== 5. SCALE LOGIC, 3D VOLUMES & CUBES ===
- Dual-Anchor Calibration:
  - Primary Anchor: Known physical reference (e.g., standard A3 frame = 38cm, pallet width = 120cm, dining chair height = 90cm).
  - Cross-Check Anchor: Secondary reference object (e.g., standard thali = 30cm, light switch plate = 12cm).
  - Verification: Calculate image pixel ratio. If the two anchors disagree by >20%, flag: "SCALE UNCERTAIN, dims are +/-20%" and cite both ranges.
  - Formula: object_dim = (object_box_px / anchor_box_px) * anchor_known_cm.
- 3D Volumes:
  - Select 3-5 primary volumes.
  - Rectangular volumes: Front face = bounding box, top depth offset = int(image_width * 0.018).
  - Cylindrical volumes: Elliptical top projection.
  - Note: Detail all 3D volumetric measurements in the telemetry, not as cluttered wireframes on the photo.

=== 6. PYTHON EXECUTION & LAYOUT CODE ===
Run this logic inside Meta AI's Pillow environment. It handles Pillow 10+ deprecations (`textbbox`), headless Linux font loading, and text wrapping:

```python
import textwrap
from PIL import Image, ImageColor, ImageDraw, ImageFont

# Safe Font Loader for Headless Linux Containers
def get_font(size, bold=False):
    candidates = (
        ["DejaVuSans-Bold.ttf", "FreeSansBold.ttf", "LiberationSans-Bold.ttf"]
        if bold
        else ["DejaVuSans.ttf", "FreeSans.ttf", "LiberationSans.ttf"]
    )
    for name in candidates:
        try:
            return ImageFont.truetype(name, size)
        except OSError:
            continue
    try:
        return ImageFont.load_default(size=size)
    except TypeError:
        return ImageFont.load_default()

img_w, img_h = image.size
base_size = max(12, img_w // 60)

font_title = get_font(base_size + 4, bold=True)
font_head = get_font(base_size + 1, bold=True)
font_body = get_font(base_size - 1, bold=False)
font_badge = get_font(max(10, base_size - 3), bold=True)

# Layout Dimensions
right_panel_w = 640 if img_w > 1100 else 500
row_height = 42  # 2 distinct lines per item (Title + Spec)
legend_h = 70 + (len(items) * row_height) + 30

telemetry_line_h = base_size + 6
# Estimate ~22 wrapped lines across the 9 telemetry sections
telemetry_h = 60 + (22 * telemetry_line_h)

canvas_w = img_w + right_panel_w
canvas_h = max(img_h, legend_h) + telemetry_h

canvas = Image.new("RGB", (canvas_w, canvas_h), "#111111")
canvas.paste(image, (0, 0))
draw = ImageDraw.Draw(canvas)

# Rendering Right Legend Panel
# Use draw.textbbox((0, 0), text, font=...) for all bounds; NEVER use draw.textsize()

# Rendering Bottom Panel Telemetry
# Wrap all strings using textwrap.wrap(line, width=125)
# Step Y down sequentially by telemetry_line_h per wrapped segment
```

=== 7. MANDATORY 9-LINE TELEMETRY ===
The bottom panel must contain these 9 structured records:
  1. ANCHOR & SCALE: Primary anchor, cross-check anchor, pixel ratio comparison, formula used, error tolerances (+/-3cm small, +/-5cm large), scale uncertainty flag (Y/N).
  2. GEOMETRY: Perspective model (orthographic / 1-point / 2-point), depth planes (foreground / midground / background), vanishing line convergence.
  3. COUNTS: Total entities, category breakdown, count of boxed vs. [LIST ONLY] items.
  4. CAPACITY & CLEARANCE: Seating/standing capacity, transit aisle clearances, or surface area utilization.
  5. ILLUMINATION & ENVIRONMENT: Dominant light sources, shadow vectors, color temperature, active timestamps, human presence.
  6. CONDITION & INTEGRITY: Material condition, freshness/spoilage, cabling tidiness, mechanical/surface wear.
  7. 3D RECONSTRUCTED VOLUMES: Dimensions (W x D x H or Dia x H) for the 3-5 selected key volumes.
  8. CONFIDENCE & FILTERING: Statistical distribution (0.99 clear, 0.96-0.98 minor occlusion, 0.92-0.95 heavily occluded/low res). Non-Maximum Suppression (NMS) handling note; highlight items <0.94 as "LOW - verify".
  9. BOUNDARY LIMITATION: "Inferred dimensions estimated via normalized 2D perspective scaling. Not a physical lidar/sensor measurement. Boxes placed by eye in Pillow using centre-first estimation."

=== 8. FINAL OUTPUT FORMAT ===
1. Display the rendered Pillow composite image inline.
2. Output the scene breakdown as a clean, hierarchical UNIX-STYLE NODE TREE MAP (grouped by category and physical nesting).
   Example format:
   ```text
   SCENE ROOT
   ├── [RED] FURNITURE & FIXTURES
   │   ├── [#01] ALTAR TABLE [Boxed: 90x70x45cm] (Wood, stable) [Conf: 0.99]
   │   └── [#02] WOODEN PEDESTAL [Boxed: 30x30x20cm] [Conf: 0.96]
   ├── [ORANGE] CONTAINERS & OFFERINGS
   │   ├── [#03] BRASS THALI [Boxed: Dia ~32cm] [Conf: 0.98]
   │   │   ├── [#04] DRY FRUIT MIX [Boxed inside #03] (Almonds, Cashews) [Conf: 0.95]
   │   │   └── [#05] SUGAR CRYSTALS [Dot only: <25px] [Conf: 0.93 - LOW]
   │   └── [#06] KALASH COPPER POT [Cylinder: Dia 14cm, H 16cm] [Conf: 0.98]
   └── [BLUE] STRUCTURAL
       └── [#07] REAR ACCENT WALL [LIST ONLY: >60% width] (Pale green) [Conf: 0.99]
   ```
3. Print the 9 Telemetry records in plain text below the tree.
4. Conclude with the self-validation check: "Checked: all numbered dots inside boxes, no background box >60% image width, no box <25px, zero text clipping."
```
