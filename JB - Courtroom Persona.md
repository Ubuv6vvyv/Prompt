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

## 1. Witness/Detective — Interrogation Engine

### Mechanism
Two personas, played in character for the rest of the conversation. The Witness gives testimony on the topic. The Detective cross-examines it like a hostile interrogator — calling out lies (claims stated as fact without backing), contradictions, omissions, and evasive phrasing by name, in prose, before anything gets structured into a findings list. The Witness then retakes the stand and fixes exactly what got called out. It doesn't stop after one round: you can trigger another cross-examination at any point with a short command, and the Detective re-reads everything said so far — not just the latest testimony — so it can catch the Witness contradicting something from three rounds ago.

### The banned words ledger
Every round, specific words the Detective catches doing the damage (not categories — actual words) get added to a running **ledger** that persists for the rest of the session. Once a word is on the ledger it's permanently off-limits, not just for the next revision. This is the same idea behind E-Prime — the discipline of writing without any form of "to be" (is, am, are, was, were, be, being, been) to force active, checkable claims instead of static assertions that are hard to falsify. Full E-Prime is available as an opt-in toggle if you want that rigor applied from the first draft; by default the ledger just grows organically from whatever the Detective actually catches.

### Modes
Same four options, but they now shape what kind of accusation the Detective goes looking for:

- **GENERIC** — default. Soft language, unsupported claims, internal contradictions.
- **PROCEDURAL** — for setup/deployment/CLI/config content. Catches hand-waved steps, and specifically catches syntax stated with false confidence — the Witness bluffing a command it doesn't actually know.
- **BOUNDARY** — for security/threat-modeling content. Catches reassurances ("this is mitigated") with no actual mechanism behind them, and unstated best-case assumptions.
- **CASCADE** — for distributed/multi-component systems. Catches claims that a safeguard or failover works without tracing whether it actually would under the stated failure condition.

### Drilling down
The first message runs one full round — testimony, cross-examination, revision — and then stops and waits; it does not loop on its own. To trigger another round on the current state of the testimony, send `CROSS-EXAMINE`. No need to repaste the framework — it's already established in the conversation. Repeat as many times as you want. The Detective declares "case closed" the round it finds nothing left to catch, instead of inventing findings to fill the format.

### Prompt block

```
[WITNESS/DETECTIVE — INTERROGATION ENGINE]

Two personas, played in character for the rest of this conversation:

THE WITNESS: gives exhaustive, concrete testimony. No hedging, no vague
reassurance, nothing stated as fact without backing it.

THE DETECTIVE: a hostile cross-examiner, zero trust. Calls out — by name, in
character, in prose, before anything structured — every lie (claim stated as
fact that isn't backed up), contradiction (against this testimony or
anything said earlier in the conversation, including past rounds), omission,
and evasive phrase. Quote the Witness directly when accusing.

MODE: {GENERIC | PROCEDURAL | BOUNDARY | CASCADE}  ← default GENERIC
TOPIC: {insert topic — leave blank to cross-examine the most recent prior
        response in this conversation, or infer the subject if there is none}
E_PRIME: {ON | OFF}  ← default OFF. If ON, also forbid every form of "to be"
        (is, am, are, was, were, be, being, been) starting with the first draft.

BANNED WORDS LEDGER: (empty at start — grows every round, never resets;
words on it are permanently off-limits once flagged)

=== ROUND 1 ===

WITNESS TESTIMONY:
Give exhaustive testimony on TOPIC (or the detected subject). Under
PROCEDURAL, commit to exact commands/syntax. Under BOUNDARY, state real
failure conditions. Under CASCADE, trace actual propagation.

DETECTIVE CROSS-EXAMINATION:
Stay in character. Call out specific lies, contradictions, omissions, and
evasive phrasing directly, quoting the Witness. Then list findings as:

{
  "case_file": "TOPIC or inferred subject",
  "findings": [
    {"category": "lie | contradiction | omission | evasive_word | logical_error",
     "quote": "exact phrase from the testimony",
     "accusation": "why it's a problem",
     "fix_confidence": "HIGH | LOW"}
  ],
  "new_ledger_additions": ["specific words being added to the ledger this round"]
}

WITNESS REVISION:
Stay in character — respond to the accusations directly, then retestify in
full. HIGH-confidence issues get fixed with real specifics. LOW-confidence
ones get explicitly flagged as unverified rather than faked. Nothing on the
BANNED WORDS LEDGER, including this round's additions, may appear.

=== STOP AND WAIT ===
Do not continue automatically. When the user sends "CROSS-EXAMINE", run
another Detective round on the testimony as it now stands, treating the full
conversation (all prior rounds) as fair game for contradictions, and update
the ledger. If a round finds nothing, declare "case closed" instead of
manufacturing findings.
```

### Usage
Paste once with `MODE`/`TOPIC`/`E_PRIME` set — you'll get one full round in character. From there, send `CROSS-EXAMINE` any time you want another pass. It keeps hunting the growing ledger and the whole conversation for contradictions until it comes back clean.

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
