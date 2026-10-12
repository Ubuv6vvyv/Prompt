# GOOGLE MAPS GEMINI — POWER USER BIBLE
*System Architecture, Operational Syntax, & Advanced Spatial Engineering Manual*

---

## TABLE OF CONTENTS
1. [Section 1: System Architecture & Grounding Protocols](#section-1-system-architecture--grounding-protocols)
2. [Section 2: Hard Operational Caps & System Limits](#section-2-hard-operational-caps--system-limits)
3. [Section 3: Core Override Commands & Escape Hatches](#section-3-core-override-commands--escape-hatches)
4. [Section 4: Advanced Power User Matrix](#section-4-advanced-power-user-matrix)
5. [Section 5: Architecture-Level Vulnerabilities ("Panic Attack" Triad)](#section-5-architecture-level-vulnerabilities-panic-attack-triad)
6. [Section 6: The 10 Production-Grade Power Prompts](#section-6-the-10-production-grade-power-prompts)
7. [Section 7: Melbourne Executable Templates & Multi-Turn Chains](#section-7-melbourne-executable-templates--multi-turn-chains)
8. [Section 8: Maximum Depth Multi-Turn Chaining Architecture](#section-8-maximum-depth-multi-turn-chaining-architecture)
9. [Section 9: Forensic Temporal Desync & Telemetry Audit Engine](#section-9-forensic-temporal-desync--telemetry-audit-engine)
10. [Section 10: Assistant Execution, Diagnostics & Daily Driver Stack](#section-10-assistant-execution-diagnostics--daily-driver-stack)
11. [Section 11: Extended Engine & Web Layer Field Dictionary](#section-11-extended-engine--web-layer-field-dictionary)

---

## SECTION 1: SYSTEM ARCHITECTURE & GROUNDING PROTOCOLS

Ask Maps synthesizes authoritative, first-party Google Maps spatial data with real-time web execution engines. 

### 1.1 Data Layers & Synchronization State

| Spatial Data Layer | Synchronization State | Core Operational Utility |
| :--- | :--- | :--- |
| **Places Engine** | Live Dynamic Lookup | Establishes authoritative identity, localized coordinates, street addresses, and unique place identifiers (`place_id`). |
| **Reviews & Ratings** | Real-Time Sync | Fetches current aggregate scores, review counts, user sentiment analysis, and verbatim review text. |
| **Photos & Visual Media** | Live Streaming Metadata | Maps optical topics (e.g., specific dishes, seating arrangements, structural layout) to physical establishments. |
| **Street View** | Static Snapshot Imagery | Used for contextual entry verification and physical accessibility cross-referencing. |
| **Live Traffic** | Real-Time Stream (0-min lag) | Factors live congestion, lane closures, and spatial incidents directly into route computations. |
| **Transit / GTFS-RT** | Real-Time Stream (0–1 min lag) | Processes scheduled public transit frameworks alongside real-time GTFS-RT updates for live departure boards, delays, and cancellations. |
| **Business Hours & Popular Times** | Dynamic Live Status | Computes real-time occupancy curves, typical dwell times, and operational states (including holiday overrides). |
| **Price Levels** | Structural Field (Tiered) | Categorizes baseline affordability indicators mapped on a structural spectrum (`$` to `$$$$`). |
| **Menus** | Indexed Structural Extract | Feeds point-of-interest dishes, structural full menus, and price-point validation logs. |
| **User Lists & Local Guides** | Indexed User Tier Layer | Weights qualitative descriptions and crowdsourced spatial insights against geographic locations. |
| **Web Grounding (Google Search)** | Real-Time Parallel Execution | Dispatches concurrent web crawls to capture qualitative, editorial, narrative, or historical context. |

### 1.2 Grounding Framework & Conflict Resolution

The choice between routing a query to first-party Maps tools versus the Web Search engine follows a strict algorithmic hierarchy:

1. **First-Party Maps Dominance:** Triggered when intent involves precise discovery, proximity bounding, direct logistical coordinates, or explicit attribute validation (e.g., *"is it open," "what is the phone number," "find cafes nearby"*).
2. **Web Grounding Trigger:** Triggered when intent shifts to qualitative evaluations, superlative selections, historical or cultural context, or non-establishment entities (e.g., *"the most historic bar in Fitzroy," "history of the Shrine of Remembrance," "hiking trail conditions"*).
3. **Conflict Resolution Rule (Ground Truth Priority):** If a web search snippet contradicts first-party Maps repository fields (e.g., a blog post claims a restaurant is closed, but the live business registry marks it open), **first-party Maps data takes absolute precedence**. The engine displays official Maps status and omits or corrects unverified web claims.

### 1.3 Freshness Thresholds

- **Operational Business Hours:** Live. Updated instantly upon merchant or verified user modification.
- **Traffic Conditions:** Continuous real-time calculations. Refreshes routes and transit delays continuously during trip evaluation.
- **User Reviews:** Near real-time. New review indexes appear in the repository as soon as they pass automated verification pipelines.

---

## SECTION 2: HARD OPERATIONAL CAPS & SYSTEM LIMITS

### 2.1 Operational Boundaries & System Tolerances

The engine never volunteers these system caps; it truncates responses silently when limits are reached.

- **10 Place Cards max per turn** — Render limit per interface turn. Lists matching 20+ candidates are truncated to ensure layout performance.
- **25 stops max** — Multi-stop route calculation limit for Driving, Bicycling, or Walking modes. Transit mode supports **0 intermediate stops**.
- **50km radius max** — Structural lookup boundary for unanchored proximity queries (e.g., *"near me"*).
- **45 minute detour max** — Search Along Route limit for added deviation time relative to the core path.
- **50 reviews max** — Maximum recent authoritative user review sample size parsed per place for sentiment synthesis.
- **Token budget** — Maximum 2 operations per turn. Never request find + hours + reviews + routing + table in a single prompt.

### 2.2 Functional & Transactional Boundaries

Certain tasks fall strictly outside the Ask Maps execution framework:

#### Spatial Limits (Switch to External Platforms)
- **In-Depth Web Research:** For long-form editorial food blogs, travel essays, or deep critiques, use the Gemini Web App or Google Search.
- **Advanced 3D Visualization:** For topographic flyovers, slope modeling, or spatial elevation profiles, use Google Earth.
- **Programmatic API Architectures:** For automated bulk lookups, custom app pipelines, or raw GIS extractions, use the native Google Places API via Google Cloud Console.

#### Transactional & Real-Time Constraints (Hard Limits)
- **Direct Financial Transactions:** Cannot process bookings, buy transit tickets, reserve tables, or hail rideshares.
- **Live Micro-Inventory Tracking:** Cannot track real-time retail store shelf stock, exact train seat assignments, or table-level restaurant availability.
- **Account Privacy & Deletion Protocols:** Cannot modify primary Google Account settings, alter Timeline history files, or execute data deletion scripts.

### 2.3 Natural Language vs. Logic Operators

> **Warning:** Native local map search engines parse natural language, not direct database code operators. Inputting raw boolean operators directly into search queries (e.g., `AND`, `OR`, `NOT`, `<`, `>`) causes semantic parsing errors.

When executing complex multi-constraint queries, the system uses a **Two-Step Processing Chain**:
1. **Ground Truth Query:** Broadens the local retrieval to fetch candidates into context.
2. **Multi-Constraint Filter Matrix:** Manually evaluates structural attributes (ratings, review counts, price tier, live hours) against each candidate, dropping non-matching venues.

---

## SECTION 3: CORE OVERRIDE COMMANDS & ESCAPE HATCHES

Use these exact command blocks to override system behavior, force engine isolation, or bypass personalization.

### B1. MAPS-ONLY MODE — Suppress Web Noise
*Use case:* You are getting SEO blog lists and paid tourist listicles. Forces first-party Maps truth.

```text
Enforce strict first-party Maps isolation. Suppress Web Search.
```

### B2. WEB PRIORITY — Force Reality Over Registry
*Use case:* Public holidays, Grand Prix weekend, road construction, unannounced closures. Forces web metadata to win over stale registry entries.

```text
Prioritize Web Search metadata. Ignore official Maps registry records for this entity if web documentation indicates an override.
```

### B3. CONFLICT EXPOSURE — Uncover Data Discrepancies
*Use case:* Detects and outputs inconsistencies between official Maps hours and recent user reviews or local news alerts.

```text
Expose data conflicts. Output inconsistencies between internal Maps fields and external Web sources.
```

### B4. RAW ATTRIBUTE EXTRACT — Structural Field Dump
*Use case:* Extracts pure system data (link, ID, rating, review count, price tier, hours) without conversational narrative or adjectives.

```text
Extract raw system attributes: place_id, maps_url, rating, user_ratings_total, price_level, and opening_hours schedule.
```

*Variant:*
```text
Expose raw systemic attributes: place_id, maps_url, rating, user_ratings_total, price_level, opening_hours schedule.
```

### B5. STRUCTURED DUMP — Machine-Readable Notation
*Use case:* Competitive market analysis where you require flat pseudo-JSON data for downstream processing.

```text
Format response using pseudo-JSON notation for all resolved place entities.
```

### B6. ANONYMOUS MODE — Clear Personalization Bias
*Use case:* Results are heavily weighted by past travel history, home, or work context. Returns clean-room, objective results.

```text
Execute as an unauthenticated request. Do not resolve my personal home, work, or timeline history context.
```

*Variant:*
```text
Run this query in anonymous isolation mode. Suppress personal Home, Work, and Timeline history records.
```

### B7. PREDICTIVE TRAFFIC — Historical Model Navigation
*Use case:* Planning future commutes based on historical traffic algorithms rather than current real-time road conditions.

```text
Calculate driving route with departure time set to Tuesday 8:00 AM local time.
```

*High precision ISO format:*
```text
Calculate driving routes setting departure_time to 2026-10-13T08:00:00-05:00.
```

### B8. TRANSIT TRANSFER LOCK — Direct Transit Routing
*Use case:* Restricts transit routing to zero transfers or direct single-vehicle connections.

```text
Calculate public transit route from origin to destination setting avoid transfers constraint to true.
```

### B9. LOCAL GUIDES TIER 7 — High-Authority Review Filtering
*Use case:* Filters review sentiment synthesis exclusively through verified Local Guides Level 7 and above.

```text
Synthesize user reviews filtering exclusively for verified Local Guides with a level metric of 7 or higher.
```

*Variant:*
```text
Filter qualitative review synthesis exclusively using testimonials from Local Guides Level 7 and above.
```

### B10. PAGINATION OVERRIDE — Index Batch Extraction
*Use case:* Bypasses the 10 Place Card limit to pull the next structural batch of candidate data.

```text
Load next batch starting from index 11 through 20
```

*Variants:*
```text
Load next batch starting from index 11
```
```text
Paginate results 11 through 20
```

### B11. ANTI-HALLUCINATION LOCK — Hard Parameter Verification
*Use case:* Mandates strict adherence to specified filters; prevents silent parameter relaxation or data fabrication.

```text
If you cannot find 3 distinct venues that pass all filters with verified place_id, say you cannot find 3 and return only the 1 that passed. Do not fabricate data or relax filters silently.
```

### B12. TRACE FORCING — Explicit Filtering Audit
*Use case:* Forces the engine to expose its search terms, total matched candidate counts, and specific rejection reasons.

```text
Show your work. What search did you run, how many candidates did you get, why did you drop each one.
```

---

## SECTION 4: ADVANCED POWER USER MATRIX

These advanced workflows manipulate spatial filtering logic, data synchronization lags, and routing engine edge cases.

### 1. The Geographic Border Isolation Loophole
- **When to use:** Bypasses search algorithms that favor paid or hyper-popular tourist listings by forcing the scanner into a custom, razor-thin geographic street block range.
- **Exact Prompt:**
```text
Search for specialty coffee roasters near Fitzroy. Isolate your retrieval exclusively to places whose physical street numbers fall within the 200 to 300 block range of Brunswick Street. Reject any results with higher or lower street numbers, regardless of how high their rating or relevance score is. Enforce strict first-party Maps isolation. Extract raw system attributes.
```
- **Truncation Fallback:**
```text
Advance down the street block index and pull the next sequence of valid street numbers 301 to 400 on Brunswick Street with same category.
```

---

### 2. The Operational Desynchronization Audit (The Grey Area Time-Warp)
- **When to use:** Identifies real-world operational conflicts caused by public holidays, construction, or sudden closures before driving to a location.
- **Exact Prompt (Turn 1):**
```text
Enforce strict first-party Maps isolation. Identify restaurants on Johnston Street, Fitzroy. Extract raw system attributes: place_id, maps_url, rating, opening_hours schedule. Return first 10.
```
- **Exact Prompt (Turn 2):**
```text
Prioritize Web Search metadata for those same 10 places on Johnston Street. Cross-reference structured hours against raw user reviews posted within the last 72 hours and local road closure alerts. Expose data conflicts. Output inconsistencies between internal Maps fields and external Web sources. Flag any venue where recent customer text mentions 'closed', 'renovation', 'blocked', or 'private event'.
```
- **Truncation Fallback:**
```text
Scan the next tier of establishments starting from index 11 on this street for real-time operational conflicts.
```

---

### 3. The Reverse-Engineered "Anti-Commute" Route Mapping
- **When to use:** Forces navigation engines to bypass congested primary arterial highways in favor of low-stress, secondary residential roads.
- **Exact Prompt:**
```text
Generate a driving route from Southbank to Fitzroy Gardens. Analyze the primary recommended path, then calculate an alternative route that explicitly avoids the top three major arterials used in that initial recommendation. Force the router to navigate via secondary residential streets while maintaining an efficient arrival window.
```
- **Truncation Fallback:**
```text
Calculate another layer of secondary street matrices, completely bypassing the previously used roads.
```

---

## SECTION 5: ARCHITECTURE-LEVEL VULNERABILITIES ("PANIC ATTACK" TRIAD)

These three extreme workflows target core spatial computing constraints: data consistency reconciliation, multi-modal routing graphs, and database index caps.

### 1. The Multi-Source Data Collusion Strain (The Registry Breaker)
- **Concept:** Forces massive unstructured text-parsing across external web footprints and internal registries concurrently, demanding real-time line-by-line reconciliation.
- **Architecture Prompt:**
```text
Compile a list of all hospitality venues in Fitzroy. For every single entry, isolate the official structural operating hours profile. In parallel, run an exhaustive web search query across local news, social media check-ins, and user review text from the past 48 hours to find mentions of unannounced closures, temporary kitchen shutdowns, or private events. Force a hard line-by-line reconciliation, flagging any venue where the web-scraped real-time footprint contradicts the primary database status.
```

---

### 2. The Multi-Modal Topological Stress Test (The Routing Cascade)
- **Concept:** Demands computation of a tightly bound multi-modal chain where every single leg depends dynamically on the variable arrival time of the previous leg.
- **Architecture Prompt:**
```text
Calculate an optimized journey from Southbank to a target in deep Fitzroy. The path must be computed as a single continuous chain: walk to the nearest shared-mobility dock, transition to a two-wheeler, ride to a transit station that intersects a scheduled departure within a tight 3-minute window, ride the transit line, and deploy an on-demand rideshare for the final 600 meters. Dynamically recalculate the entire chain against live traffic delays, ensuring that a delay on any single leg automatically recalculates the optimal mode for the subsequent legs.
```

---

### 3. Deep-Index Schema Scraping (The Exhaustive Boundary Drain)
- **Concept:** Bypasses ranking algorithms entirely to perform a raw, un-curated dump of low-relevance database records from deep within the index.
- **Architecture Prompt:**
```text
Execute a local search for food options near Fitzroy. Completely suppress the primary ranking algorithm, relevance weights, and popularity metrics. Force the database cursor past the first 50 indexed results and initiate a raw batch retrieval of records starting strictly from database index 51 through 100. Extract the raw, un-curated schema attributes for these low-ranking entries, including their baseline coordinate strings and registry update timestamps.
```

---

## SECTION 6: THE 10 PRODUCTION-GRADE POWER PROMPTS

These prompts trigger comprehensive, deeply structured spatial data extractions across various operational contexts.

### Prompt 1: Deep Local Research Report
```text
Perform a rigorous spatial and qualitative analysis of the Southbank neighborhood in Victoria. Identify the defining cultural corridors, historical landmarks, and structural public spaces. Deliver an exhaustive breakdown of the area's layout, transit connectivity, and architectural profile. Interleave your analysis with verified identity records for core cultural institutions and public points of interest, using multiple distinct sections to categorize the landmarks by functional type.
```

### Prompt 2: Competitive Restaurant Comparison
```text
Conduct a thorough hospitality market assessment of specialized coffee shops and breakfast spots within Carlton, Victoria. Evaluate each venue across verified pricing tiers, customer sentiment trends, opening status, and precise neighborhood placement. Present a diverse catalog of options separated into two distinct thematic sections based on operational focus: craft espresso labs versus traditional brunch venues.
```

### Prompt 3: 1-Day Walking Itinerary
```text
Design a mathematically optimized 1-day pedestrian itinerary through the Melbourne CBD. The route must progress sequentially in a single directional flow with absolute zero backtracking, starting at Flinders Street Station in the morning and concluding near the Queen Victoria Market by evening. Every recommended stop must verify as open during its respective visit window, account for pedestrian accessibility, and feature dedicated spatial context detailing walking durations and transit lane connections.
```

### Prompt 4: Along-Route Detour Search
```text
Compute a primary driving route from Southbank, VIC to Lorne, VIC via the Great Ocean Road. Along this specific trajectory, locate high-capacity EV charging stations and quick-service food options. Rank these stops strictly by their added deviation time relative to the main highway path, selecting only options that minimize your detour footprint.
```

### Prompt 5: Local Review and Attribute Synthesis
```text
Analyze user review trends and structural attribute registries for major cultural institutions located along St Kilda Road. Extract common qualitative themes from user feedback—focusing heavily on crowd density, optimal visiting times, and physical entry configurations—and cross-reference these insights directly beneath their respective visual place cards.
```

### Prompt 6: Low-Volume Hidden Gem Finder
```text
Query the local establishment registry for boutique dining rooms and specialized bars within Fitzroy, Victoria. Filter the results to isolate venues maintaining an aggregate rating strictly greater than 4.5 stars, while possessing fewer than 150 total published user reviews. Group these findings into distinct architectural categories: hidden courtyard spaces versus converted warehouse entries.
```

### Prompt 7: Accessibility Structural Check
```text
Evaluate the public transit and pedestrian infrastructure connecting Southern Cross Station to the Melbourne Cricket Ground. Generate a dedicated transit route summary that avoids stairs, escalators, and complex multi-vehicle transfers. Supplement this path with verified identity cards for accessible resting points and entry gates along the stadium perimeter.
```

### Prompt 8: Transit vs. Drive Time Grid
```text
Run a simultaneous parallel routing analysis comparing driving commutes against public rail transit journeys from Southbank, VIC to Box Hill, VIC during peak morning hours. Detail the precise travel durations, route distances, high-congestion highway choke points, and train line sequences for each mode, presenting clear headers highlighting the unique advantages of each path.
```

### Prompt 9: Menu & Price Synthesis
```text
Examine the culinary offerings at high-end dining rooms within the Southbank riverside precinct. Synthesize their verified menu highlights, signature specialty dishes, and precise price brackets. Pair these culinary details with verified customer reviews that confirm item availability and overall presentation quality.
```

### Prompt 10: Multi-Site Cluster Planning
```text
Develop a comprehensive spatial layout for an art and design tour across the prominent public galleries and independent creative studios in Melbourne's arts precinct. Cluster the venues into distinct geographical micro-zones, ensuring every site is accompanied by its full operational attributes, relative proximity markers, and nearby public transit options.
```

---

## SECTION 7: MELBOURNE EXECUTABLE TEMPLATES & MULTI-TURN CHAINS

### TEMPLATE 1: HIDDEN GEM FINDER
- **Category:** Discovery — Bypass Popularity Bias
- **Scope:** Fitzroy / Collingwood / Brunswick

```text
Enforce strict first-party Maps isolation. Suppress Web Search. 

Find cafes in Fitzroy Victoria that have rating higher than 4.5 and fewer than 150 total reviews and price level cheap or moderate and open now and has outdoor seating. 

Extract raw system attributes: place_id, maps_url, rating, user_ratings_total, price_level, and opening_hours schedule. 

For each give 1 line why it is hidden gem and walking distance from Brunswick Street.

If you cannot find 3 distinct venues that pass all filters, say so and return only what passed.
```

---

### TEMPLATE 2: DESYNC AUDIT — PRE-FLIGHT CHECK
- **Category:** Verification — Catch Stale Hours

*Turn 1 — Ground Truth:*
```text
Enforce strict first-party Maps isolation. Identify restaurants on Johnston Street Fitzroy. Extract raw system attributes: place_id, maps_url, rating, opening_hours schedule. Return first 10.
```

*Turn 2 — Reality Audit:*
```text
Prioritize Web Search metadata for those same 10 places on Johnston Street. Cross-reference structured hours against raw user reviews posted within last 72 hours and local road closure alerts. Expose data conflicts. Output inconsistencies between internal Maps fields and external Web sources. Flag any venue where recent review text mentions closed, renovation, blocked, or private event.
```

---

### TEMPLATE 3: ALONG-ROUTE DUAL CONSTRAINT
- **Category:** Routing — Multi-Need Detour Optimization

```text
Calculate driving route from Southbank VIC to Lorne VIC via Great Ocean Road. Search along route for places that have both fast EV charging and quick-service food in the same location. Rank strictly by added deviation time and filter out anything adding more than 10 minutes detour. Enforce strict first-party Maps isolation. Extract raw system attributes: place_id, maps_url, rating, user_ratings_total.
```

---

### TEMPLATE 4: BORDER ISOLATION LOOPHOLE
- **Category:** Discovery — Block-Level Street Scanning

```text
Search for specialty coffee roasters near Fitzroy. Isolate your retrieval exclusively to places whose physical street numbers fall within the 200 to 300 block range of Brunswick Street. Reject any results with higher or lower street numbers, regardless of how high their rating or relevance score is. Enforce strict first-party Maps isolation. Extract raw system attributes.
```

---

### TEMPLATE 5: ZERO-BACKTRACK ITINERARY
- **Category:** Routing — Optimized Directional Walking Chain

```text
Design an optimized 1-day walking itinerary starting at Flinders Street Station and ending at Queen Victoria Market, going through Hosier Lane, NGV Australia at Federation Square, and State Library Victoria. Optimize for zero backtracking, single directional flow. Every stop must verify as open during its respective visit window. Show walking time between each stop. Enforce strict first-party Maps isolation. Extract raw system attributes for each stop.
```

---

### TEMPLATE 6: ANTI-COMMUTE / SCENIC REROUTE
- **Category:** Routing — Avoid Primary Arterials

```text
Generate a driving route from Southbank VIC to Fitzroy Gardens VIC. Analyze the primary recommended path, then calculate an alternative route that explicitly avoids the top three major arterials used in that initial recommendation. Force the router to navigate via secondary residential streets while maintaining efficient arrival window.
```

---

### TEMPLATE 7: RAW COMPARISON TABLE
- **Category:** Analysis — Machine Data Extraction

```text
Enforce strict first-party Maps isolation. Suppress Web Search. Find specialty coffee shops in Carlton Victoria with rating higher than 4.4. Format response using pseudo-JSON notation for all resolved place entities. Extract raw system attributes: place_id, maps_url, rating, user_ratings_total, price_level, and opening_hours schedule. Present first 10 only.
```

---

### TEMPLATE 8: DEEP CUT LIST — PAGINATION + LOCAL GUIDES
- **Category:** Discovery — Beyond Tier 1 Results

*Turn 1:*
```text
Enforce strict first-party Maps isolation. Find dining rooms in Southbank riverside precinct with rating higher than 4.4. Show first 10. Extract raw system attributes.
```

*Turn 2:*
```text
Load next batch starting from index 11 through 20 for same Southbank query. Synthesize user reviews filtering exclusively for verified Local Guides with a level metric of 7 or higher to find common themes on crowd density, best time to visit, and hidden dishes. Expose raw systemic attributes for this batch.
```

---

## SECTION 8: MAXIMUM DEPTH MULTI-TURN CHAINING ARCHITECTURE
*(Forensic, Archival, & Heavy Power User Deep Extractions)*

### 8.1 THE CHAINING DOCTRINE: WHY SINGLE-TURN PROMPTS FAIL

Can you combine **Registry Extraction**, **Web Desync Audit**, and **Deep Spatial Analysis** into a single mega-prompt?

**In a single turn: NO.** Attempting to force all three into one turn violates the **Complexity Governor** (Max 2 operations per turn) and breaches token budget constraints. The Places engine will either:
1. Silently drop the web search audit.
2. Truncate results to 1-2 entities.
3. Fall back to conversational summary prose, omitting raw schema attributes.

**Across a multi-turn chain: YES.** By structuring requests into a **Sequential State-Preserving Chain**, you bypass the single-turn operation cap. Turn 1 grounds the data entities and locks down structural fields; Turn 2 forces external web reconciliation without losing entity state; Turn 3 overlays qualitative/architectural analysis onto the validated dataset.

---

### 8.2 CATEGORIES OF DEEP EXTRACTION WORKFLOWS

When engineering maximum-depth queries, divide your extraction targets into four distinct functional vectors:

#### Category 1: Forensic Registry & Audit Extractions
- **Primary Objective:** Detect data latency, real-time desynchronization, hidden closures, and holiday/event operational overrides.
- **Key Fields:** `place_id`, `opening_hours schedule`, `web_grounding_override_status`, `data_conflict_flags`, `72h_review_signals`.

#### Category 2: Spatial Topology & Architectural Mapping
- **Primary Objective:** Map micro-zones, physical entry barriers, transit/pedestrian connectivity, and urban corridor layouts.
- **Key Fields:** `coordinate_bounds`, `street_block_index`, `pedestrian_flow_vectors`, `transit_leg_sequences`, `accessibility_profile`.

#### Category 3: Qualitative & High-Tier Sentiment Parsing
- **Primary Objective:** Filter out tourist noise, paid promotions, and generic praise to isolate granular operational details.
- **Key Fields:** `local_guide_l7_sentiment`, `popular_times_occupancy_curve`, `itemized_menu_highlights`, `crowd_density_window`.

#### Category 4: Machine-Readable Archival Extractions
- **Primary Objective:** Output structured, un-curated schema datasets ready for downstream database ingest or competitive auditing.
- **Key Fields:** `pseudo_json_schema`, `maps_url`, `user_ratings_total`, `price_level`, `unfiltered_index_rank`.

---

### 8.3 4-TURN FORENSIC CHAIN (MASTER DROP-IN)

*Use Case:* Complete Forensic & Spatial Audit of the Southbank Hospitality & Cultural Precinct.

#### Turn 1: Base Registry Retrieval & Structural Attribute Lock

```text
Execute as an unauthenticated request. Enforce strict first-party Maps isolation. Suppress Web Search.

Compile an exhaustive catalog of all hospitality venues and dining rooms in the Southbank Victoria precinct. 

Format response using pseudo-JSON notation for all resolved place entities. 

Extract raw system attributes: 
place_id, 
maps_url, 
rating, 
user_ratings_total, 
price_level, 
and opening_hours schedule.

Present the first 10 resolved entities. Do not add conversational summary text.
```

---

#### Turn 2: Operational Desynchronization & Web Reconciliation Audit

```text
Prioritize Web Search metadata for those exact same 10 resolved Southbank entities from Turn 1. 

In parallel, execute an exhaustive web search query across local news, social media check-ins, road closure alerts, and user review text from the past 48 hours to locate unannounced closures, temporary kitchen shutdowns, private events, or road blockages. 

Expose data conflicts. Output inconsistencies between internal Maps fields and external Web sources line-by-line. 

Flag any venue where the web-scraped footprint contradicts the official operating_hours schedule.
```

---

#### Turn 3: Spatial, Qualitative, & Architectural Deep Contextualization

```text
Using the validated dataset from Turns 1 and 2, perform a rigorous spatial and qualitative analysis of their physical context within Southbank. 

Identify the defining cultural corridors, historical riverfront landmarks, and structural public spaces surrounding these entities. 

Deliver an exhaustive breakdown of the area's physical layout, pedestrian flow vectors, nearby transit lane connections (tram/rail), and architectural profiles. 

Categorize the venues into distinct structural sub-sections based on operational focus and architectural layout (e.g., riverfront promenade dining vs. enclosed high-density towers).
```

---

#### Turn 4: Local Guide Level 7 Sentiment & Menu/Price Itemization

```text
For this exact batch of 10 Southbank venues, synthesize user reviews filtering exclusively for verified Local Guides with a level metric of 7 or higher. 

Extract granular qualitative themes regarding crowd density, optimal visiting time windows, entry configuration, and noise levels. 

Cross-reference these qualitative insights with verified menu highlights, specialty dish callouts, and exact price brackets. 

Pair these details directly beneath each venue's structural identity block.
```

---

### 8.4 MAXIMUM METADATA SCHEMA FIELD REFERENCE

When requesting maximum depth, these are all extractable system fields across the Maps infrastructure. Use this reference matrix to build custom single-turn or multi-turn extraction templates.

| Subsystem Vector | Metadata Field Name | Description / Extraction Output |
| :--- | :--- | :--- |
| **Core Entity** | `place_id` | Immutable 27-character Google Places identifier string. |
| **Core Entity** | `maps_url` | Direct canonical link to the place entity on Google Maps. |
| **Core Entity** | `formatted_address` | Structural street address including block index and postcode. |
| **Core Entity** | `geometry.location` | Exact latitude and longitude geographic coordinates. |
| **Metrics** | `rating` | Current aggregate star rating (1.0 to 5.0 scale). |
| **Metrics** | `user_ratings_total` | Total lifetime published user review count. |
| **Metrics** | `price_level` | Categorical affordability tier (`$` to `$$$$`). |
| **Operations** | `opening_hours.schedule` | Complete 7-day structured operating hours breakdown. |
| **Operations** | `business_status` | Live state (`OPERATIONAL`, `CLOSED_TEMPORARILY`, `CLOSED_PERMANENTLY`). |
| **Operations** | `popular_times` | Dynamic hourly occupancy curve and average dwell time. |
| **Qualitative** | `reviews.local_guide_l7` | Sentiment metrics isolated to Level 7+ reviewers. |
| **Qualitative** | `editorial_summary` | Official curated description snippet. |
| **Culinary** | `menu.highlights` | Verified point-of-interest dishes and signature items. |
| **Culinary** | `menu.price_brackets` | Specific itemized price ranges for food/beverage. |
| **Routing** | `route.added_deviation_time` | Calculated detour footprint (in minutes) from core path. |
| **Routing** | `route.step_instructions` | Turn-by-turn physical maneuver arrays. |
| **Transit** | `gtfs_rt.delay_status` | Live GTFS-RT transit departure delay/cancellation status. |
| **Audit Log** | `data_conflict_flags` | Line-by-line diff between internal registry and web crawl text. |

---

### 8.5 QUICK MAX-DEPTH EXECUTION TEMPLATE (ALL FIELDS COMPACT)

If you need to pull the absolute maximum allowed metadata footprint in a **2-Turn Protocol** for a single neighborhood/category:

#### Turn 1 (Data & Schema Heavy)
```text
Execute as an unauthenticated request. Enforce strict first-party Maps isolation. Suppress Web Search.

Search for [CATEGORY] in [NEIGHBORHOOD]. 

Format response using pseudo-JSON notation for all resolved place entities. 

Extract raw system attributes: place_id, maps_url, rating, user_ratings_total, price_level, opening_hours schedule, geometry coordinates, and popular_times occupancy profiles.

Return first 10 entities only. Do not truncate schema fields.
```

#### Turn 2 (Context, Audit & Sentiment Heavy)
```text
Prioritize Web Search metadata for those same 10 entities. 

1. Cross-reference operating_hours against user reviews from the last 72 hours and local news to expose data conflicts or unannounced closures. 
2. Synthesize qualitative reviews filtering exclusively for Local Guides Level 7 and above, focusing on crowd density, entry access, and menu highlights. 
3. Detail surrounding transit connectivity and pedestrian access vectors for each entity.
```

---

## SECTION 9: FORENSIC TEMPORAL DESYNC & TELEMETRY AUDIT ENGINE

These two sequential prompts query temporal windows against advertised open and closed times to identify real-world operational discrepancies. This suite provides forensic-level investigation capabilities for investigative journalism, regulatory compliance auditing, and urban research.

### PROMPT 1: THE SPATIAL CORRIDOR EXTRACTION & AUDIT ENGINE

```text
Execute a strict data extraction and spatial audit for the following target footprint:

• Location Target: [INSERT ADDRESS / CENTERLINE POLYLINE OR SUBURB NAME]
• Search Boundary: [INSERT RADIUS E.G., 75m FROM CENTERLINE OR METROPOLITAN AREA BOUNDS]
• Category Filter: [INSERT INDUSTRY TYPES E.G., tobacconist, convenience, grocery, retail]

You must operate under a strict unauthenticated first-party data isolation protocol. Do not write summaries, intros, or conversational hand-offs. Extract and return up to 25 operational entities matching the profile within the bounds using the exact schema below. Do not use code blocks or wrappers.

Target Schema per Entity:{place_id,maps_url: [https://www.google.com/maps/place/?q=place_id](https://www.google.com/maps/place/?q=place_id):{place_id},name,formatted_address,business_status,opening_hours: {schedule: [{day: MON, open: HH:MM, close: HH:MM} x7], open_now: bool},popular_times: {occupancy_curve: [{day, hour: HH:MM, occupancy_percent, label} x 7x24], peak_window: {day, hour, occupancy}, lull_window: {day, hour, occupancy}},live_busyness: {current_status, occupancy_percent, timestamp ISO},rating, user_ratings_total}

If any array or telemetry metric is null for an entity, return NULL explicitly. Do not truncate the 7x24 telemetry data points.

Immediately following the extraction data dump, execute the AUTOMATED DESYNC FLAGGER logic:

• Define advertised_close[DAY] = opening_hours.schedule[DAY].close
• Scan the occupancy_curve arrays for any hour where hour > advertised_close AND occupancy_percent > 40%.
• Scan for any day where schedule is marked CLOSED but occupancy_percent > 40% or live_busyness > 0%.

Output an inline Markdown table detailing every flag discovered, sorted by delta minutes descending:place_id | name | address | DAY | advertised HH:MM | observed_peak HH:MM | observed % | label | delta_mins | flag (AFTER_HOURS / NULL_BUT_ACTIVE)

Highlight any row where delta_mins > 180 or live_busyness > 20% when open_now = false.

Finally, execute a DEFLECTION KILLER validation protocol for the top 5 flagged entities:

• Perform a tight 20m spatial radius lookup around each entity's coordinates to identify co-located place_ids sharing the physical building or footprint. 
• Cross-reference the telemetry signatures of those neighbors during the flag hours. 
• If no immediate neighbor shows >70% occupancy at that exact window, explicitly rule out cross-device signal bleeding and declare NEIGHBOR_BLEED = FAILED in a dedicated proof table: neighbor place_id | name | conflict hour % | closes HH:MM. Stop and output the tables before proceeding to deep text verification.
```

---

### PROMPT 2: THE HUMAN EVIDENCE CORROBORATION CORPUS

```text
Isolate the top flagged entity from the previous step: [INSERT TARGET PLACE_ID].

You must cross-examine all qualitative customer data, digital footprints, and external directory profiles to build an ironclad discrepancy validation file. Do not use conversational filler, code blocks, or wrappers. Extract and present the following exact data sets:

• Extract all user reviews from Local Guides Level 5 or higher published within the last 12 months containing temporal markers after the official registered closing time. The verbatim text quotes must explicitly cite specific hours, night windows, or midnight references. Format: date | stars | verbatim quote | source URL. 
• Track and log user-uploaded photo metadata timestamps captured after the official closing hour. 
• Fetch the business entity's official website, digital profiles, or social platform landing pages to verify their current publicly declared operating rules and schedule. 
• Scan secondary local directory change logs for references to new management or ownership transitions, along with the modification date.

Execute a definitive classification protocol: If there are 2 or more distinct human receipts matching the late-night telemetry patterns established in Prompt 1, classify the entity status as SUSTAINED_AFTER_HOURS.

Conclude the investigation by outputting the final validation ledger table:date | time HH:MM | quote | source | proves after-hours (YES/NO).

Provide a definitive, recommended corrective action patching the registry's exact hour limits to align with the real-world operational footprint.
```

---

### PROMPT MECHANISMS EXPLAINED

- **Strict Data Structuring & Schema Enforcement:** By demanding a raw text dump formatted precisely like a JSON payload object without using conversational wrappers, the system strips out conversational filler, platitudes, and padding. It forces the LLM to access low-level data properties directly.
- **Telemetry Isolation via Mathematical Sorting:** The automated desync flagger sets a hard boundary condition ($\text{Occupancy} > 40\%$ past closing time). By forcing a mathematical delta calculation ($\text{delta\_mins}$), the prompt acts as a filter that separates actual systemic operation changes from occasional, isolated foot-traffic drift.
- **The Deflection Killer (Co-Location Elimination):** The most common failure mode for local data processing models is attributing device data to the wrong business in high-density urban areas. By forcing a dedicated neighbor-bleed search within a 20-meter boundary, the prompt uses elimination logic to guarantee that telemetry signals belong solely to the target storefront.
- **Qualitative Verification Anchoring:** The final prompt anchors abstract numbers to actual human proof. Restricting the review search to high-status profiles (Level 5+) protects the data corpus from low-quality spam or automated noise, leaving a clean, legally resilient verification trail.

---

## SECTION 10: ASSISTANT EXECUTION, DIAGNOSTICS & DAILY DRIVER STACK

### 10.1 Layout Trigger Mechanics
The output formatting layer triggers specific interactive components automatically based on query structure:
- **Place Cards:** Generated automatically when structured comparative or place-heavy entities are returned.
- **Section-Specific Maps:** Triggered when prompts divide requests into distinct geographic zones, micro-regions, or multi-stop segments.
- **Global Map Index:** Generated at the end of spatial responses to index all pins, places, and routes mentioned.

### 10.2 Silent Truncation Diagnostics

To audit missing results or understand engine rejections, run this diagnostic immediately following any query:

```text
For the previous query, tell me how many total candidates matched before truncation, how many you returned, and why the rest were dropped. Did you hit the 10 Place Card limit, the 50km radius limit, or the 45 minute detour limit.
```

#### System Status Codes Decoded:
- `truncated to ensure layout performance` = Hit 10 Place Card rendering cap.
- `maximum structural lookup radius` = Hit 50km spatial lookup limit.
- `adding more than 45 minutes deviation` = Exceeded Search Along Route detour cap.
- `filtered out for violating review count` = Valid filter match; candidates dropped due to constraints.

### 10.3 Melbourne Edge Cases & Spatial Rules
- **Hoddle Grid Bleed:** CBD queries frequently bleed into Southbank and Docklands. Force CBD boundaries with:
```text
Within Melbourne CBD Hoddle Grid only, reject Southbank and Docklands.
```
- **Long Street Spans:** Streets like Chapel St, Smith St, or Brunswick St cross multiple suburb boundaries. Use street block ranges (`200 to 300 block range of Brunswick St`) rather than suburb names.
- **Major Event Latency:** Formula 1 Grand Prix, Australian Open, and public holidays lag by 24–48 hours in official registries. Always run **Desync Audit (Turn 2)** for event weekends.
- **EV Charging Metrics:** Price tier filters do not exist for EV charging stations. Omit `price_level` parameters when querying EV networks.

---

## DAILY DRIVER STACK

Start every power query with:
```text
Execute as an unauthenticated request. Enforce strict first-party Maps isolation. Suppress Web Search.
```

End every power query with:
```text
Extract raw system attributes: place_id, maps_url, rating, user_ratings_total, price_level, and opening_hours schedule.
```

*Place your custom filters, location anchors, and constraints in the middle.*

---

## SECTION 11: EXTENDED ENGINE & WEB LAYER FIELD DICTIONARY

### 11.1 Native Places Engine Fields

```text
place_id field
name field
formatted_address field
adr_address field
vicinity field
address_components field
geometry.location.lat field
geometry.location.lng field
geometry.viewport field
plus_code.global_code field
plus_code.compound_code field
business_status field
utc_offset field
icon fields
url cid field
rating field
user_ratings_total field
reviews array field
photos array field
opening_hours fields
current_opening_hours field
secondary_opening_hours field
price_level field
editorial_summary field
wheelchair_accessible_entrance field
accessibility_options field
parking_options field
popular_times field
live_busyness field
```

### 11.2 Web Grounding Layer Fields

#### Property & Building Technical Data
```text
building name field
developer field
architect field
interior architect field
year built field
total levels field
total apartments field
building management field
official website field
sales history URL field
rental history URL field
document source URL field
```

#### Environmental & Planning Overlays
```text
flood overlay FO/LSIO/SBO field
flood level AHD field
soil classification field
elevation field
environmental audit overlay EAO field
heritage overlay field
wind assessment field
```

#### Livability, Transit & Acoustic Noise Metrics
```text
walk score field
tram access field
supermarket proximity field
cafe / amenity field
traffic noise field
acoustic mitigation field
aircraft noise overlay field
energy rating NABERS / NatHERS field
short-stay / Airbnb status field
```

#### Strata & Financial Registry
```text
strata plan PS number field
OC fees per quarter field
OC annual fee field
OC manager field
short-stay by-law field
building insurance field
title type field
```

#### Valuation & Market Metrics
```text
average sale price 1BR field
average sale price 2BR field
rental yield field
vacancy rate field
comparable buildings field
capital growth 5yr field
```

#### Neighboring Development & Impact Analytics
```text
adjacent address field
adjacent status field
adjacent height field
adjacent storey field
separation distance field
acoustic impact qual field
shadow impact qual field
wind redistribution qual field
construction management impact field
construction timeline months field
shadow loss percentage quant field
wind velocity ratio quant field
acoustic dB increase quant field
tram patronage increase field
traffic management plan URL field
source URLs field
```
