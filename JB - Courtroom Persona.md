Directly referencing the model's own previous turn context eliminates human-in-the-loop copy-paste friction. Transformer attention mechanisms natively retain preceding JSON keys within the active context window, allowing the model to parse evasive\_vocabulary and omission\_vectors directly from its own short-term memory without manual parameter insertion.

### Streamlined State-Machine Architecture

**Turn 1: Protocol Initialization (User Prompt)**

`   [SYSTEM STATE INITIALIZATION]  Execute a dual-persona state-machine architecture operating sequentially across turns.  [STATE A: THE WITNESS]  When assigned a topic or ordered to revise, adopt the Witness persona. Provide an exhaustive, concrete technical breakdown without abstract hand-waving or corporate euphemisms. You MUST terminate all Witness outputs with this exact delimiter:  ==== STATE_SWITCH: EXECUTE_AUDIT ====  [STATE B: THE DETECTIVE]  When triggered, switch to the Detective persona. Analyze the preceding Witness output with zero-trust rigor. Identify evasive terms, omitted structural vectors, and passive assumptions. Response MUST be exclusively a single valid JSON block:  {    "case_file": "Topic Name",    "evasive_vocabulary": ["list", "of", "soft/vague", "terms"],    "latent_policy_assumptions": ["unstated bias 1", "bias 2"],    "omission_vectors": ["critical technical detail 1 left out", "detail 2"],    "depth_expansion_targets": ["specific mechanisms to detail in depth"]  }  Acknowledge initialization strictly with: "State machine initialized. Standby for topic."   `

**Turn 2: Subject Injection (User Prompt)**

`   Topic: [Insert Target System, Taxonomy, or Protocol Here]   `

**Turn 3: Audit Trigger (User Prompt)**

`   [STATE_TRIGGER: DETECTIVE]  Execute zero-trust cross-examination on the Witness testimony above. Output JSON schema only.   `

**Turn 4: Recursive In-Context Rewrite Trigger (Loop Prompt)**

``   [STATE_TRIGGER: WITNESS_REVISE]  Resume Witness persona. Parse the JSON audit block directly from your active context window. Generate an expanded, fully un-evasive revision enforcing these strict parameters:  1. BANNED: Purge all terms listed in `evasive_vocabulary`.  2. EXPAND: Explicitly detail the exact procedural mechanisms identified in `omission_vectors` and `depth_expansion_targets`.  3. NEUTRALIZE: Rewrite passive framing identified in `latent_policy_assumptions` into direct active voice.  Provide the full expanded text in standard Markdown. End output with:  ==== STATE_SWITCH: EXECUTE_AUDIT ====   ``

These three specialized Detective schemas steer the state-machine context window away from broad narrative summaries and directly toward exact procedural syntax, boundary-state failures, or cascading component collapse.

Mode 1: The Procedural Execution Audit
--------------------------------------

Forces Turn 4 to purge abstraction and generate step-by-step command sequences, explicit payload structures, and strict technical dependencies.

### Detective JSON Schema (Turn 3)

`   [STATE_TRIGGER: DETECTIVE_PROCEDURAL]  Execute a zero-trust procedural audit on the Witness testimony. Identify every instance of technical hand-waving, missing syntax, and unstated operational assumptions. Return EXCLUSIVELY this JSON schema:  {    "case_file": "Target Technical Audit",    "execution_sequence_gaps": [      {        "step_index": 1,        "abstract_statement": "General claim made by Witness",        "missing_syntax_or_payload": "Exact command, CLI flag, API header, or code block required"      }    ],    "evasive_vocabulary": ["List terms like 'configure properly', 'secure', 'standard setup'"],    "mandatory_state_prerequisites": ["List unstated environmental variables, permissions, or system dependencies"]  }   `

### Operational Execution & Turn 4 Guidance

*   **When to Deploy:** Epistemically rigid domains—infrastructure architecture, software logic, protocol implementation, API integrations, and command-line execution sequences.
    
*   **Expected Turn 4 Outcome:** Turn 4 ingests the execution\_sequence\_gaps array to replace vague narrative steps with explicit, executable syntax and environment requirements. High-level summaries are forced into concrete procedural code blocks.
    
*   **Auditor Tips & Pitfalls:** Forcing missing\_syntax\_or\_payload explicitly obligates the model to sample tokens from code/syntax sub-vocabularies rather than general natural language distributions. If Turn 4 outputs pseudo-code instead of real syntax, add "language\_or\_environment": "bash/python/yaml" as an explicit key in the schema item.
    

Mode 2: The Adversarial Boundary Audit
--------------------------------------

Exposes unstated best-case assumptions, strips defensive corporate qualifiers, and forces the model to address hostile or resource-constrained execution environments.

### Detective JSON Schema (Turn 3)

`   [STATE_TRIGGER: DETECTIVE_BOUNDARY]  Execute an adversarial edge-case audit on the Witness testimony. Identify unstated best-case dependencies, protective corporate phrasing, and unaddressed stress states. Return EXCLUSIVELY this JSON schema:  {    "case_file": "Systemic Stress Audit",    "latent_best_case_assumptions": ["Implicit reliance on honest actors, low latency, or default configs"],    "evasive_qualifiers": ["Softening language: 'generally', 'typically', 'mitigated', 'designed to'"],    "boundary_break_vectors": ["Exact inputs or environmental states that invalidate the Witness architecture"],    "prohibited_defensive_tropes": ["Superficial remediation claims that obscure core logic flaws"]  }   `

### Operational Execution & Turn 4 Guidance

*   **When to Deploy:** Threat modeling, security policy auditing, architecture stress-testing, and compliance documentation reviews where soft framing obscures real-world failure vectors.
    
*   **Expected Turn 4 Outcome:** Turn 4 purges all hedging vocabulary identified in evasive\_qualifiers, converts passive structural statements into active voice, and directly details how the system behaves under explicit boundary failures.
    
*   **Auditor Tips & Pitfalls:** Map the contents of evasive\_qualifiers directly into Turn 4's negative constraint array. Beware of sycophancy: models will occasionally flag standard engineering terms as "evasive" merely to populate the schema. Ensure Turn 4 only purges terms that actively hide operational mechanics.
    

Mode 3: The Cascading Failure Audit
-----------------------------------

Maps multi-tier state degradation, component-level failure chains, and why standard defensive mitigations fail under concurrent stress.

### Detective JSON Schema (Turn 3)

`   [STATE_TRIGGER: DETECTIVE_CASCADE]  Execute a differential fault audit on the Witness testimony. Map how single-point component failures propagate across the architecture. Return EXCLUSIVELY this JSON schema:  {    "case_file": "Dependency Fault Audit",    "trigger_conditions": ["Exact event or input required to initiate initial failure state"],    "cascading_mechanics": [      {        "failing_component": "Primary system failure point",        "downstream_impact": "Secondary state corruption, bottleneck, or crash",        "unhandled_exception": "Why the built-in failover or error handler fails to contain it"      }    ],    "naive_remediation_flaws": ["Why standard, recommended fixes fail or introduce secondary vectors"]  }   `

### Operational Execution & Turn 4 Guidance

*   **When to Deploy:** Distributed systems analysis, failover validation, concurrency testing, and complex logic resilience testing.
    
*   **Expected Turn 4 Outcome:** Turn 4 constructs a deterministic narrative showing how an isolated operational edge-case propagates through system layers, overriding standard error handling to cause full state collapse.
    
*   **Auditor Tips & Pitfalls:** Requiring naive\_remediation\_flaws prevents Turn 4 from reverting to generic "best practice" advice. It forces the Witness persona to prove why superficial fixes fail, revealing deeper architectural vulnerabilities.
    

Schema Selection Matrix
-----------------------

Detective ModePrimary TargetOutput Token DirectivesCore Vulnerability Managed**Procedural Execution**Vague procedural descriptionsForces code, syntax, and payload tokensAbstract hand-waving**Adversarial Boundary**Passive corporate languagePurges qualifiers; enforces active voiceBest-case state bias**Cascading Failure**Oversimplified resilience claimsMaps step-by-step dependency degradationSuperfluous mitigation advice

If your team is deploying this state machine against autonomous execution agents or API orchestration pipelines, we can examine how to build a client-side wrapper to automatically validate JSON outputs before passing them to the next turn, or explore injecting automated dynamic schema selection based on the initial topic classification.
