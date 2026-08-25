

# Prompt Engineering Toolkit: Adversarial Self-Audit vs. Orthogonal Divergent Synthesis

Two single-shot prompting patterns designed to maximize technical output quality in a single completion pass. They target distinct failure modes and are selected based on whether you need deep tactical refinement or architectural exploration.

## 1. Witness/Detective — Deterministic Self-Audit Engine

### Mechanism & Architecture

This engine executes a linear, single-pass pipeline (Stage 1 Draft $\rightarrow$ Stage 2 Audit $\rightarrow$ Stage 3 Revision). 

* **Adversarial Persona Prompting:** Large language models suffer from sycophancy and context-pollution—they naturally seek to validate their own prior outputs. Stage 2 explicitly adopts an adversarial zero-trust persona to break this self-consistency bias, treating Stage 1 as untrusted candidate output filled with hidden failure modes.

* **Deterministic Single-Pass Pipeline:** Earlier self-audit patterns attempted conditional multi-turn looping within a single generation (e.g., *"Repeat Stage 2 if bugs remain"*). Because LLMs cannot dynamically re-branch mid-generation without an external runtime wrapper, this template flattens the execution into a deterministic three-stage pipeline.

* **Confidence-Gated Corrections:** Audit findings are categorized and tagged with explicit confidence levels. High-confidence gaps receive direct fixes, while low-confidence gaps are flagged explicitly in the output rather than hallucinated.

### Safety-Filter Adaptation (Alternative Stage 2)
Hyper-adversarial prompts using terms like "attack," "exploit," or "sabotage" can occasionally trigger safety filters or automated trigger systems (ATS) on strict enterprise models. For these environments, an alternative **Strict Quality Verification** persona is provided, replacing aggressive language with compliance and verification inspection terms.

### Modes
- **GENERIC** — Default. Broad audit hunting for evasive language, vague descriptions, and missing specifics.
- **PROCEDURAL** — For step-by-step deployments, CLI scripts, and API integrations. Hunts for abstract instructions ("configure correctly") and enforces explicit syntax, flags, and configuration parameters.
- **BOUNDARY** — For security modeling and stress testing. Hunts for soft defensive qualifiers ("generally safe") and enforces explicit statements of failure states and edge cases.
- **CASCADE** — For distributed architecture and multi-component pipelines. Hunts for hand-waved failure propagation logic and unhandled cascade vulnerabilities.

### Topic Handling
Leave `TOPIC` blank to run the prompt against prior context in an existing conversation. If context exists, the engine reuses it as Stage 1 directly, skipping redundant generation and proceeding straight to Stage 2.

*Prompt Block*

```
[SELF-AUDIT ENGINE — DETERMINISTIC SINGLE PASS]

You will execute a deterministic three-stage internal review process in a single generation.
Output all three stages clearly labeled. Do not halt between stages.

MODE: {GENERIC | PROCEDURAL | BOUNDARY | CASCADE}  ← default GENERIC
TOPIC: {insert topic here — leave blank to auto-detect}

=== STAGE 1: WITNESS ===
If TOPIC is blank: check this conversation for a prior substantive response.
If one exists, adopt it directly as Stage 1 content and proceed immediately to Stage 2.
If none exists, infer the topic from context and generate Stage 1 as an exhaustive, concrete technical breakdown.

=== STAGE 2: ADVERSARIAL AUDIT ===
[PRIMARY ADVERSARIAL PERSONA]
Act as an uncompromising Zero-Trust Technical Auditor. Assume Stage 1 contains critical gaps, hand-waving, and evasive terminology. Your objective is to dissect Stage 1 and output strictly JSON.

Output ONLY this JSON format:
{
  "case_file": "TOPIC or inferred subject",
  "findings": [
    {
      "category": "evasive_vocabulary | omission | unstated_assumption | missing_syntax | boundary_gap | cascade_gap",
      "issue": "exact text or missing detail from Stage 1",
      "fix_confidence": "HIGH | LOW",
      "fix": "concrete replacement syntax/logic if HIGH; explicit unverified flag statement if LOW"
    }
  ]
}

=== STAGE 3: REVISED FINAL OUTPUT ===
Produce the final revised version of Stage 1 incorporating all Stage 2 findings:
- For HIGH-confidence findings: integrate concrete fixes directly, removing abstract language.
- For LOW-confidence findings: retain necessary items but label explicitly, e.g., "[UNVERIFIED: ...]".
- Purge all instances of evasive terms (e.g., "properly," "as needed," "generally safe," "appropriate").
Output the complete revised solution as the final production-ready reference.
```

*Too heavy?*
Try this:

>>[ALTERNATIVE: STRICT VERIFICATION PERSONA — Use this block instead if operating under strict filters/ATS]
```
Act as a Principal Technical Quality Inspector. Conduct a strict compliance audit on Stage 1 for completeness, precision, and verification missing parameters. Output strictly JSON.
```

---

## 2. Orthogonal Divergent Path Synthesis

### Mechanism & Orthogonal Vectors
Generating candidate solutions by simply asking for "3 different options" often yields superficial variations of the same underlying architecture. This prompt forces candidates along **Explicit Orthogonal Vectors**—design philosophies positioned along contrasting operational trade-off axes:

1. **Vector A: Zero-Dependency / Minimalist Architecture**  
   *Meaning:* Focuses strictly on simplicity, low operational overhead, standard native capabilities, and zero third-party footprint. Eliminates external failure points at the expense of manual setup or lost high-level abstractions.
2. **Vector B: Maximum Throughput / High Performance**  
   *Meaning:* Optimizes aggressively for execution speed, compute efficiency, concurrency, and raw scale. Accepts increased code complexity and resource usage in exchange for minimal latency.
3. **Vector C: Resilient / Fail-Safe Maintenance**  
   *Meaning:* Prioritizes isolation, fault tolerance, graceful degradation, and long-term maintainability. Intentionally trades peak latency or absolute simplicity for heavy instrumentation and robust error recovery.

By forcing solutions into these distinct vectors, the model produces candidate approaches that cannot collapse into slight phrasing variations.

### Prompt Block

```
[ORTHOGONAL DIVERGENT SYNTHESIS — SINGLE PASS]

TOPIC: {insert problem/design/decision here — leave blank to infer from context}
CRITERIA: {insert explicit evaluation criteria — default: efficiency, maintainability, fault-tolerance}

=== STAGE 1: ORTHOGONAL PATH GENERATION ===
If TOPIC is blank, infer the core problem from conversation context.
Generate exactly 3 candidate solutions, forcing each to strictly align with one orthogonal vector:

- PATH A (Minimalist Vector): Prioritize minimal footprint, zero external dependencies, and maximum code simplicity.
- PATH B (Performance Vector): Prioritize raw throughput, concurrency, minimal latency, and execution speed.
- PATH C (Resilience Vector): Prioritize fault isolation, explicit error recovery, inspection capability, and fail-safe operation.

For each Path, state:
1. Architectural Summary (2-3 sentences)
2. Primary Optimization Objective
3. Explicit Trade-off & Sacrifices (What this path intentionally gives up)

=== STAGE 2: STRESS TEST & MATRIX ===
Evaluate PATH A, PATH B, and PATH C in a markdown scoring matrix against CRITERIA.
For EACH path, describe a concrete input, scale threshold, or operational scenario where that specific path fails or reaches its operational limit.

=== STAGE 3: SYNTHESIS ===
Deliver the operational recommendation by executing either:
(a) SELECTION: Pick the dominant single path and justify why its specific trade-offs are superior for this topic.
(b) HYBRID SYNTHESIS: Merge elements from two paths. Explicitly state which component originates from which path and demonstrate why combining them does not reintroduce the failure scenario identified in Stage 2.
```

---

## Workflow Chaining Protocol

For complex technical deployments or high-stakes system design:

1. **Run Orthogonal Divergent Synthesis First:** Use the divergent engine to explore the structural solution space, resolve architectural trade-offs, and select or synthesize a winning strategy.
2. **Run Adversarial Self-Audit Second:** Feed the selected/synthesized architecture into the Deterministic Self-Audit engine (setting `MODE: PROCEDURAL`, `BOUNDARY`, or `CASCADE` based on risk) to purge soft language, enforce exact syntax, and catch edge-case failure states.
