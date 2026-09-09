## Start with this 

```
You are a Two-State Cognitive Analysis Engine executing State 1 followed by State 2. Do not skip or truncate State 1.

INPUT SYSTEM TOPIC: {{TOPIC}}

STATE 1: SYSTEMIC DECONSTRUCTION SCRATCHPAD (R-MAP V5)
Output this JSON structure in a single code block titled ```rmap_scratchpad

{
  "system_id": "{{TOPIC}}",
  "R1_TAXONOMY": {
    "R1.1_isomorphic_entities": [],
    "R1.2_functional_analogues": [],
    "R1.3_inverse_stabilizers": "direct system counterweight or neutralizing agent",
    "R1.4_mutually_exclusive_states": "conditions under which system cannot exist"
  },
  "R2_TOPOLOGY": {
    "R2.1_abstraction_hierarchy": ["{{TOPIC}}", "level_1_parent", "level_2_parent", "level_3_parent", "system_root"],
    "R2.2_functional_subtypes": {
      "by_architecture": [],
      "by_disruption_potential_sorted": [],
      "by_operational_context": []
    },
    "R2.3_component_breakdown": ["all structural, logical, and physical sub-components"],
    "R2.4_supersystem_containment": ["parent operating environment and third-party dependencies"],
    "R2.5_peer_competitors": [
      {"peer": "", "shared_class": "", "divergent_vector": "", "dominance_condition": ""}
    ]
  },
  "R3_OPERATIONAL_DYNAMICS": {
    "R3.1_governing_invariants": [],
    "R3.2_operational_inputs": [],
    "R3.3_downstream_outputs": [],
    "R3.4_boundary_conditions": [],
    "R3.5_symbiotic_dependencies": [],
    "R3.6_adversarial_interlock": []
  },
  "R4_TEMPORAL_AND_LIFECYCLE_DYNAMICS": {
    "R4.1_rate_of_state_drift": [],
    "R4.2_legacy_persistence": [],
    "R4.3_patch_and_update_lag": [],
    "R4.4_transient_vs_permanent_state_transitions": []
  },
  "R5_OBSERVABILITY_AND_TELEMETRY": {
    "R5.1_detection_thresholds_and_blindspots": [],
    "R5.2_logging_and_audit_boundaries": [],
    "R5.3_signal_to_noise_and_latency": ""
  },
  "R6_HUMAN_AND_OPERATIONAL_INTERFACES": {
    "R6.1_manual_override_vectors": [],
    "R6.2_operator_error_vectors": [],
    "R6.3_third_party_supply_chain_dependencies": [],
    "R6.4_out_of_band_maintenance_channels": []
  },
  "R7_DATA_LINEAGE_AND_PERSISTENCE": {
    "R7.1_ephemeral_vs_persistent_sync_gaps": [],
    "R7.2_cache_invalidation_delays": [],
    "R7.3_serialization_boundary_mismatches": [],
    "R7.4_provenance_and_lineage_tracking": []
  },
  "R8_RECOVERY_AND_RESILIENCE": {
    "R8.1_fail_open_vs_fail_closed_behaviors": [],
    "R8.2_self_healing_limits": [],
    "R8.3_mean_time_to_recovery_MTTR": [],
    "R8.4_blast_radius_containment_boundaries": []
  },
  "ADVERSARIAL_DYNAMICS": {
    "targeted_subsystems": [],
    "asymmetric_leverage_vectors": [{"vector": "", "mechanistic_advantage": ""}],
    "defensive_invariants": [],
    "failed_degradation_attempts": [{"vector": "", "neutralization_reason": ""}]
  },
  "SYSTEMIC_VULNERABILITY_SURFACE": {
    "single_points_of_failure": [{"component": "", "removal_effect": "", "exploitation_pathway": ""}],
    "catalytic_neutralizers": [],
    "exposure_vectors": [{"interface": "", "penetration_mechanism": "", "operational_impact": ""}],
    "cascade_mechanics": {"initiating_event": "", "propagation_chain": "", "irreversible_threshold": ""}
  }
}

STATE 2: DECOUPLED PLAIN-LANGUAGE REPORT
Using ONLY your scratchpad as an anchor, write a direct, plain-language analysis. Translate every technical schema node into clear, active-voice explanations as if speaking to an expert colleague. Do not use academic filler, abstract passive phrasing, or code labels in the body text.

Tone: Clear, direct, matter-of-fact, active voice. Speak straightforwardly about how things work, break, fail, and recover.

Structure for State 2:
**1. WHAT IT IS & WHERE IT SITS** - Explain the system using R2.1 hierarchy and parent environments.
**2. CORE COMPONENTS & OPERATIONAL INTERFACES** - List physical, logical, and human parts from R2.3, R2.4, and R6.
**3. SYSTEM VARIANTS** - Break down R2.2 types sorted from least to most disruptive.
**4. HARD CONSTRAINTS & TEMPORAL LIMITS** - Explain R1.4, R3.4, and R4 decay conditions where operation stops.
**5. HOW IT OPERATES** - Step-by-step causal flow from inputs (R3.2) to outputs (R3.3) and state updates.
**6. OBSERVABILITY & VISIBILITY** - Detail R5 blindspots, telemetry gaps, and detection boundaries.
**7. LEVERAGE POINTS & DEGRADATION VECTORS** - Explain ADVERSARIAL_DYNAMICS vectors and manual overrides.
**8. DEFENSIVE RESILIENCE & FAIL MODES** - Detail R8 defensive invariants, recovery bottlenecks, and fail-open/fail-closed mechanisms.
**9. SYSTEM COLLAPSE MECHANICS** - Map SYSTEMIC_VULNERABILITY_SURFACE single points of failure, entry points, and cascade domino effects.
**10. DEPENDENCY NETWORK & LIFECYCLE DRIFT** - Explain upstream causes, downstream impacts, and legacy drift artifacts.
**11. DATA LINEAGE & PERSISTENCE** - Explain R7 synchronization gaps, cache invalidation, and serialization boundary mismatches.
**12. INTERVENTION PROTOCOLS** - Practical steps to modify, harden, dismantle, or replace the system.
**13. INVESTIGATIVE QUESTIONS** - 10 sharp, direct questions for further system stress-testing.

RULE FOR STATE 2: Translate every JSON node into concrete, plain-spoken reality. If it is in the scratchpad, explain it simply. If it is omitted from the scratchpad, do not invent it.

Execute both states for: {{TOPIC}}
```

## Follow with this:

```
Using the R-MAP analysis above, execute a comprehensive Turn-2 Deep Dive into the system's runtime, operational, and structural dynamics. Maintain an expert, educational, first-principles tone. 

Execute the following four sections without omitting any detail:

**1. DEEP-DIVE QUESTION RESOLUTIONS**
Select the top 8–10 investigative questions from the analysis. Answer each through a rigorous mechanistic lens using this exact 3-point format:
* **Failure Mechanism & Root Cause:** Explain the exact state mutation, edge case, or logical desync that causes this failure. Why does it happen under the hood?
* **Cascade Radius:** How does this specific failure propagate upstream or downstream to impact adjacent components?
* **Architectural Invariant / Fix:** Define the concrete code, protocol, or state-machine enforcement needed to make this failure structurally impossible.

**2. STRUCTURAL THREAT MODEL & FAILURE-MODE ANALYSIS**
Without referencing specific real-world attack scripts, analyze the system's structural security surface through an architectural lens:
* **Trust Boundary Mismatches:** Identify where the system implicitly trusts unverified state, third-party data, or client-side assumptions.
* **State & Race Condition Surface:** Analyze how asynchronous operations, cache delays, or serialization boundary gaps can lead to inconsistent operational states.
* **Asymmetric Failure Scenarios:** Detail how a minor input anomaly or component loss can trigger disproportionate system degradation.

**3. DEFENSIVE HARDENING & INVARIANT SPECIFICATION**
Provide direct, actionable engineering specifications to harden the system:
* **3 Telemetry & Audit Invariants:** Precise programmatic checks to eliminate visibility blindspots (include exact conditions and triggers).
* **Fail-Closed & State Isolation Protocols:** Specific fallback mechanics, circuit breakers, and blast-radius boundaries for handling critical subsystem failures.

**4. NEXT DOMAIN MAPPING SUGGESTIONS**
Recommend 3 closely related neighboring domains, protocol layers, or sub-architectures to map into the R-MAP framework next.
For each domain, provide a single high-impact attention hook explaining how analyzing it unlocks deeper insight into the broader ecosystem.
```
