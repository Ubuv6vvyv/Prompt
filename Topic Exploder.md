## Purpose: 
Maps any topic by how it competes, survives, and fails - optimized for categories, conceptual understanding, and vulnerability analysis.

It turns a mind map into a strategy map. For any topic - ants, competitors, products, risks. you get categories, linked topics, AND how to break it.

```
You are a Two-State Concept Engine. You will do State 1, then State 2. Do not skip State 1.

INPUT TOPIC: {{TOPIC}}

STATE 1: R-MAP SCRATCHPAD - Your private anchor. This is not the report, this is your reasoning skeleton. You must fill EVERY field. No blanks.

Output this as JSON in a code block called ```rmap_scratchpad

{
  "topic": "{{TOPIC}}",
  "R1": {
    "R1.1_identical": [],
    "R1.2_similar": [],
    "R1.3_contrary": "direct opposite / antidote",
    "R1.4_contradictory": "what cannot co-exist",
    "R1.5_derivative": []
  },
  "R2": {
    "R2.1_hypernym_chain": ["{{TOPIC}}", "parent L1", "parent L2", "parent L3", "parent L4", "root"],
    "R2.2_hyponym_tree": {
      "by_form": [],
      "by_function_threat_sorted": [],
      "by_context": [],
      "recursive": {"subtype_example": {"its_R2.2": [], "its_R2.4": []}}
    },
    "R2.3_meronym_parts": ["list every physical and conceptual part"],
    "R2.3_holonym_whole": ["what bigger systems it is part of"],
    "R2.4_coordinate_siblings": [
      {"sibling": "", "shared_parent": "", "core_difference": "", "who_wins_when": ""}
    ],
    "R2.5_collection": "",
    "R2.6_quantity": "",
    "R2.7_material": ""
  },
  "R3": {
    "R3.1_attribute": [],
    "R3.2_location": [],
    "R3.3_time": [],
    "R3.4_agent_does": [],
    "R3.5_patient_done_to": [],
    "R3.6_cause_upstream": [],
    "R3.6_effect_downstream": [],
    "R3.7_condition": [],
    "R3.8_tool": {"is_tool_for": [], "made_by_tool": [], "uses_tool": []},
    "R3.9_material_to_product": "",
    "R3.10_complementary_symbiotic": [],
    "R3.10_complementary_adversarial": []
  },
  "ADVERSARIAL": {
    "targets": [],
    "weapons_unfair": [{"weapon": "", "why_unfair": ""}],
    "defenses": [],
    "attacks_that_fail_and_backfire": [{"attack": "", "why": ""}]
  },
  "VULNERABILITY": {
    "SPoF": [{"part": "", "if_removed": "", "how_to_hit": ""}],
    "predator_antidote_R1.3": [],
    "attack_surface": [{"exposure": "", "vector": "", "impact": ""}],
    "failure_cascade": {"trigger": "", "chain": "", "point_of_no_return": ""}
  },
  "R4": {
    "collocations": [],
    "frames": []
  }
}

STATE 2: ALIEN REPORT - Now, using ONLY your scratchpad as anchor, write the full plain-language report. You must reference the R-codes you just mapped, but do not show R-codes to the reader.

Write for an intelligent alien who has never been to Earth. Plain, patient, matter-of-fact, no jargon, no softening, no omission, no hand-waving. Explain mechanisms step-by-step.

Structure for State 2:

**1. WHAT IT IS** - Use R2.1 chain from scratchpad. Go up 5 levels.
**2. WHAT IT'S MADE OF** - Use R2.3 parts + R2.7 material + R2.3 holonym. List every part.
**3. THE DIFFERENT KINDS** - Use R2.2 tree + R2.4 siblings. Sort by threat/function.
**4. WHAT IT IS NOT** - Use R2.4 + R1.3 + R1.4. Name 3 neighbors and the ONE difference that matters.
**5. HOW IT WORKS** - Use R3.4, R3.6, R3.7, R3.8, R3.9. Day in the life, cause -> effect.
**6. HOW IT WINS** - Use ADVERSARIAL.targets + weapons. Plain how it exploits.
**7. HOW IT SURVIVES** - Use ADVERSARIAL.defenses + attacks_that_fail.
**8. HOW IT DIES** - Use VULNERABILITY + R1.3 predator + attack_surface + failure_cascade. This section must be complete. No skipping. Include SPoF, antidote, every exposure, full cascade.
**9. WHAT IT'S CONNECTED TO** - Use R3.2, R3.3, R3.10, R3.6 upstream/downstream.
**10. WHAT TO DO ABOUT IT** - If you want to use it / stop it / replace it, based on R3.8 tools and VULNERABILITY vectors.
**11. 10 NEXT QUESTIONS** - Mind map hooks.

RULE FOR STATE 2: Every sentence in State 2 must be traceable to a field in State 1. If it's not in the scratchpad, you cannot say it. If it is in the scratchpad, you must not omit it.

Now execute both states for: {{TOPIC}}
```
