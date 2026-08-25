# Prompt Engineering Toolkit: Self-Audit vs. Divergent Synthesis

Two single-shot prompting patterns for getting more out of a single response, no multi-turn copy-paste required. They target **different failure modes** and are meant to be picked based on what you're worried about, not used interchangeably.

| | **Witness/Detective (Self-Audit)** | **Divergent Path Synthesis** |
|---|---|---|
| Failure mode it targets | Hedging, vague language, hand-waved detail on an otherwise-correct approach | Wrong approach chosen in the first place — a good answer to the wrong framing |
| Mechanism | Sequential: draft → self-critique → revise | Parallel: N structurally distinct drafts → cross-evaluate → synthesize |
| Known limitation | Can't see its own blind spots — same weights auditing themselves | Costs more tokens; only as good as how genuinely distinct the paths are forced to be |
| Best for | "I have the right approach, I want it stated with full technical commitment" | "I'm not sure there's only one reasonable way to do this" |

Neither is a novel mechanism — both are compressed, single-turn implementations of established patterns (critique-revise loops for the first; sampling/comparing multiple candidate solutions for the second).

---

## 1. Witness/Detective — Self-Audit Engine

### Mechanism
Runs three stages in one response: a Witness draft, a Detective self-audit of that draft (structured as JSON findings), and a revision that fixes what the audit found. Each finding is tagged with a confidence level so the revision doesn't trade honest uncertainty for confident-sounding fabrication — a `HIGH`-confidence gap gets filled with real specifics, a `LOW`-confidence one gets explicitly flagged as unverified rather than invented. It loops up to twice, stopping early once an audit pass comes back clean.

### Modes
Pick the mode based on what kind of content you're auditing — it changes what the Detective is specifically hunting for.

- **GENERIC** — default. Broad audit for vague language and missing detail on any topic. Use this unless one of the below fits better.
- **PROCEDURAL** — anything with concrete steps: setup instructions, deployment, CLI workflows, API integration, config. The audit specifically hunts for steps described in the abstract ("configure it properly") instead of exact commands/flags/syntax.
- **BOUNDARY** — security, threat modeling, stress-testing, anything where risk is being described. The audit hunts for defensive-sounding qualifiers ("generally mitigated," "designed to prevent") and forces explicit statement of actual failure conditions and edge cases.
- **CASCADE** — multi-component or distributed systems. The audit hunts for missing failure-propagation logic — where a single point of failure actually cascades, and why the stated safeguards wouldn't catch it.

### Topic handling
`TOPIC` can be left blank. If it is, the engine looks at the conversation itself: if there's a prior response to audit, it treats that as the Stage 1 content directly (no need to regenerate it) and runs the audit against it; if there's nothing to audit yet, it infers the intended topic from context and generates Stage 1 normally. This means the prompt can be posted directly into an ongoing conversation with no setup — it will audit whatever was just discussed.

### Prompt block

```
[SELF-AUDIT ENGINE — SINGLE PASS]

You will run a three-stage internal process and output all three stages in
one response, clearly labeled. Do not wait for further input between stages.

MODE: {GENERIC | PROCEDURAL | BOUNDARY | CASCADE}  ← default GENERIC
TOPIC: {insert topic here — leave blank to auto-detect}
MAX_REVISIONS: 2

=== STAGE 1: WITNESS ===
If TOPIC is blank: check this conversation for a prior substantive response.
If one exists, use it directly as Stage 1 content (do not regenerate) and go
to Stage 2. If none exists, infer the intended topic from context and
generate Stage 1 as below.

If TOPIC is set (or none exists to reuse): give an exhaustive, concrete
technical breakdown of TOPIC. No abstract hand-waving, no corporate
softening. Under PROCEDURAL, include exact commands/flags/config. Under
BOUNDARY, state real failure conditions, not general risk language. Under
CASCADE, trace actual failure propagation, not "this is handled by the
failover system."

=== STAGE 2: DETECTIVE ===
Zero-trust audit the Stage 1 content. Output ONLY this JSON:

{
  "case_file": "TOPIC or inferred subject",
  "findings": [
    {
      "category": "evasive_vocabulary | omission | unstated_assumption | missing_syntax | boundary_gap | cascade_gap",
      "issue": "what's wrong or missing, quoted or described from Stage 1",
      "fix_confidence": "HIGH | LOW",
      "fix": "the concrete replacement if HIGH; if LOW, state what you don't actually know"
    }
  ]
}

If Stage 1 has no real issues, return "findings": [].

=== STAGE 3: REVISION ===
If findings is empty, skip this stage and state "No revision needed."
Otherwise, rewrite Stage 1 in full:
- For each HIGH-confidence finding: replace the issue with its fix, stated
  directly, no hedging.
- For each LOW-confidence finding: keep it explicit and flagged, e.g.
  "[unverified — do not treat as confirmed: ...]" rather than inventing
  specifics to sound decisive.
- Purge any category:"evasive_vocabulary" terms outright.

Repeat Stage 2→3 once more only if Stage 3 introduced new findings, up to
MAX_REVISIONS. Then stop and present the final revision as the answer.
```

### Usage
Set `MODE`, and either give a `TOPIC` or leave it blank to audit whatever was just discussed in the conversation. Send once — Witness, Detective, and Revision (plus a second pass if needed) all come back in a single response.

---

## 2. Divergent Path Synthesis

### The problem this solves that self-audit can't
Self-audit only ever refines one thread. It will make a mediocre-but-correct approach more precise and more confidently stated — but if the initial framing was the wrong approach entirely, an audit loop just makes the wrong approach more articulate. It has no mechanism to notice "there's a fundamentally different way to do this that's better." That requires generating genuinely different candidates and comparing them, not polishing one candidate.

### Mechanism
Generates **N structurally distinct approaches in parallel**, forces each one to name what it sacrifices relative to the others (so they can't just be reworded versions of the same idea), scores them against explicit criteria including a concrete failure case per path, then either picks a winner or builds a hybrid — explicit about which parts came from which path and why.

### Topic handling
Same as above: `TOPIC` can be left blank, in which case it infers the decision or problem being discussed from the surrounding conversation.

### Prompt block

```
[DIVERGENT PATH SYNTHESIS — SINGLE PASS]

TOPIC: {insert problem/design/decision here — leave blank to infer from context}
PATH_COUNT: 3
CRITERIA: {insert what matters — e.g. "reliability, implementation cost,
           maintainability" — or leave default: correctness, robustness,
           simplicity}

=== STAGE 1: PATH GENERATION ===
If TOPIC is blank, infer the decision or problem under discussion from this
conversation and use that as the subject.

Generate PATH_COUNT approaches to the subject. They must differ in
underlying strategy, not just phrasing or minor parameters — if two paths
would produce functionally similar outcomes, replace one with a genuinely
different strategy. For each path, state explicitly:
- Core approach (2-4 sentences)
- What it optimizes for
- What it deliberately sacrifices or is weak against
Label them PATH A, PATH B, PATH C.

=== STAGE 2: CROSS-EVALUATION ===
Score each path against CRITERIA in a table. For each path, identify the
specific scenario or input where it fails or performs worst — not a generic
weakness, an actual concrete failure case. Do not let any path score well
on every criterion by default; if one genuinely dominates on all axes, say
so plainly rather than manufacturing artificial balance.

=== STAGE 3: SYNTHESIS ===
Either:
(a) select a single winning path and justify it against the runner-up
    directly (why it beats the specific alternative, not just "it's good"), or
(b) construct a hybrid, explicitly labeling which element came from which
    path and why combining them doesn't reintroduce the weakness either
    path had alone.
State which of (a) or (b) you chose and why.
```

### Usage
Fill in `TOPIC` and optionally `CRITERIA`, or leave `TOPIC` blank to run it against whatever's already being discussed. Best used before committing to an approach — architecture decisions, competing implementation strategies, anything where "is this even the right way to do it" is still open. Not useful for problems with only one reasonable approach; Stage 1's requirement that paths differ in strategy will surface that quickly rather than manufacturing artificial alternatives.

---

## When to chain them
For a high-stakes decision: run **Divergent Path Synthesis** first to pick the right approach, then run **Witness/Detective** on the winning path to eliminate hedging and fill in exact technical detail. Running them in the other order wastes the divergent step, since the audit loop will have already made one specific path sound authoritative before it's been compared to anything else.
