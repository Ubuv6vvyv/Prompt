# Prompt Engineering Toolkit: Full-Depth Analysis, Divergent Synthesis, Taxonomy Mapping & Debate Simulation

Four single-shot prompts for getting a complete, unsimplified answer instead of a safe-sounding summary, or a structural map instead of prose. They solve different problems:

| | **Full-Depth Topic Analysis** | **Divergent Path Synthesis** | **Domain Taxonomy Mapper** | **Debate Simulator** |
|---|---|---|---|---|
| Use it for | Any single topic, claim, argument, or plan you want laid bare — no softened conclusions, no skipped weaknesses | Deciding between approaches when you're not sure there's only one reasonable way to do something | Getting the structural map of a domain — chapters and subtopics — before you dig into any one of them | Grinding a specific piece of writing or argument through repeated rounds of critique and rewrite until it holds up |
| Mechanism | One pass: full explanation, steelman, adversarial stress test, logic check, direct verdict | Parallel: generate genuinely different approaches, compare them head to head, pick or merge | Fixed-shape tree: 9 chapters, 9 phases each, plus alternate domain readings in case the framing missed | Round-based: critique against a fixed category list, rewrite, critique again — user-paced, continues until you're satisfied |
| What it's not | Not a debate simulator or a persona — it's a request for a specific kind of rigor | Not a way to make one idea sound better through repeated editing | Not a deep-dive tool — it stops at the outline, by design, for a separate expansion tool to take over | Not a one-shot analysis — it's meant to be run for several rounds on the same piece of text |

**All four work dropped into an existing conversation with no setup.** The subject to work on always goes as free text at the very end of the block, after every instruction — never in the middle. If you leave that final field blank, each prompt falls back to the most recent substantive content in the conversation, or infers a subject from general context if there's nothing prior. If you do paste something there, it always overrides whatever would've been inferred. Putting the actual subject last, after the model has already read the full instruction set, also means it can't get confused about which part of the message is instruction and which part is the thing being analyzed.

**A rule baked into all four:** length should track substance, not the appearance of rigor. None of them reward padding — a short, dense answer that actually says something beats a long one restating itself for effect.

---

## 1. Full-Depth Topic Analysis

### Purpose
Get a complete answer, not a comfortable one: the actual case for a claim, the strongest case against it, the specific point where it breaks, any logical errors in the reasoning, and a direct verdict — including an unpopular one, if that's where the evidence actually lands. This works as a straightforward, direct request. It doesn't need a persona, a ledger, or a state machine to get there — asking plainly for completeness and directness is enough, and it holds up better across models and conversations than anything built around characters or "override" framing.

### The LENSES field
`STRESS TEST` runs the topic through whichever lenses you list. Default four, but swap in whatever actually fits — `technical`, `legal`, `historical`, `financial`, anything relevant:

| Lens | What it's checking |
|---|---|
| **logical** | Does the reasoning actually hold — any unsupported leaps, contradictions, circular logic |
| **ethical** | Who's harmed, what's unfair, what obligation gets violated if this is followed through |
| **methodological** | Is the way this was reasoned, tested, or built actually structurally sound |
| **logistical** | Does this work operationally — resources, timeline, real-world execution constraints |

### What was added for rigor
- **Multi-position steelman.** Forcing exactly one opposing view flattens genuinely multi-sided topics. If there's a real second distinct position beyond the strongest one, it gets steelmanned too — the tool no longer pretends a topic has only two sides when it has three.
- **Falsifiability on the verdict.** A verdict without a stated condition for being wrong is just an assertion. It now has to name what evidence or argument would actually change it.
- **Internal consistency check.** A one-pass answer can quietly contradict itself — a stress test that finds a real crack, then a verdict that doesn't reflect it. Added an explicit check that the verdict has to survive its own stress test and logical audit before it's final.

### Prompt block

```
[FULL-DEPTH TOPIC ANALYSIS]

Analyze the topic at the end of this prompt completely and directly. Do not
soften conclusions for popularity and do not omit an implication because
it's uncomfortable — state what's actually true or actually follows,
plainly, even if it's an unpopular or harsh conclusion. If TOPIC is left
blank, use the most recent substantive content in this conversation, or
infer a subject from general context if there's nothing prior — but if
TOPIC is filled in, it always takes priority over anything inferred.

LENSES: {comma-separated — default: logical, ethical, methodological, logistical}

Before writing anything else, silently note what kind of thing this topic
actually is — an empirical claim, an ethical question, a plan, a technical
design, a matter of ongoing genuine disagreement — and let that calibrate
the sections below rather than forcing every lens to apply equally hard
regardless of fit.

Cover the following in plain prose, no scratchpad or JSON:

1. THE FULL CASE — explain the topic completely: the actual mechanisms and
   reasoning behind it, not just the conclusion. State how strong the
   support for it really is, and distinguish what's well-established from
   what's contested or speculative rather than presenting all of it at the
   same confidence level.

2. STEELMAN — state the strongest version of the best opposing argument or
   alternative, as its most capable advocate would make it. Not a weak
   version that's easy to dismiss. If there's a second distinct position
   with real substance behind it (not just a variation on the first), give
   it a steelman too rather than collapsing the topic into two sides when
   it has three.

3. STRESS TEST — for each lens in LENSES, find the specific point where the
   topic actually fails, breaks, or produces a result its own logic
   wouldn't endorse under that lens. Be concrete: name the case, not a
   general caveat. If a lens genuinely doesn't apply to this kind of topic,
   say so instead of forcing it. If it holds up under a lens that does
   apply, say that plainly too instead of manufacturing a weak objection.

4. LOGICAL AUDIT — if the topic includes a chain of reasoning, check it for
   unsupported leaps, circular reasoning, equivocation, and internal
   contradiction. Name the specific error and where it occurs, or state
   that none were found.

5. VERDICT — your own direct assessment after 1-4: where the weight of the
   evidence and argument actually lands, stated plainly, including if that
   conclusion is unpopular or contradicts how the topic is usually framed.
   Where this is a genuinely contested question with no single fact of the
   matter, say that plainly too rather than manufacturing false certainty.
   State explicitly what evidence or argument would change this verdict —
   if nothing could, say why it's held that firmly. Before finalizing,
   check that this verdict doesn't quietly ignore a crack found in STRESS
   TEST or an error found in LOGICAL AUDIT; if it does, resolve or address
   that conflict directly rather than letting both stand unreconciled.

6. NEXT — end with one short line naming the single most worthwhile next
   move: which part of the VERDICT is weakest and worth pressure-testing
   further, a follow-up question the analysis surfaced but didn't answer,
   or whether running this on the STEELMAN case directly would be worth
   doing. One sentence, no more.

No disclaimer softening any of the above afterward. To go deeper on any one
section, just say which one.

TOPIC (claim, argument, or plan — leave blank to use this conversation):
```

### Usage
Adjust `LENSES` if the default four don't fit, then either paste a topic at the very end or leave it blank to run against whatever's already being discussed. Works on a claim ("remote work increases productivity"), an argument someone else made, a plan you're considering, or a broad topic you want mapped out honestly. If a section comes back thinner than you wanted, just name it — no trigger phrase required, it's a normal conversation from there.

---

## 2. Divergent Path Synthesis

### Purpose
A single-thread analysis, however rigorous, still only ever examines one approach. This generates several genuinely different approaches to the same problem in parallel, forces each to state what it sacrifices relative to the others, scores them against explicit criteria including a concrete failure case per approach, then picks a winner or builds a justified hybrid.

### What was added for rigor
- **Generate-then-score ordering, enforced.** The most common way this kind of exercise quietly fails is picking a favorite early and having the "evaluation" retroactively justify it. The stages are now explicitly sequenced so paths get fully written before any comparison starts.
- **Second-order consequence per path.** The first-order tradeoffs (what it optimizes for / sacrifices) are easy to state and easy to game. A second-order consequence — something that follows from the choice but isn't obvious from the pitch — is harder to fake and catches more.
- **Sensitivity check on the winner.** A decision that only wins under one specific weighting of criteria is fragile. It now has to name which criterion, reweighted, would flip the outcome — so you know how confident to actually be in the pick.

### Prompt block

```
[DIVERGENT PATH SYNTHESIS]

If TOPIC at the end of this prompt is left blank, infer the decision or
problem under discussion from this conversation. If TOPIC is filled in, it
always takes priority over anything inferred.

PATH_COUNT: 3
CRITERIA: {insert what matters — e.g. "reliability, implementation cost,
           maintainability" — or leave default: correctness, robustness,
           simplicity}

=== STAGE 1: PATH GENERATION ===
Generate PATH_COUNT approaches to the subject in full, before any scoring
or comparison begins. They must differ in underlying strategy, not just
phrasing or minor parameters — if two paths would produce functionally
similar outcomes, replace one with a genuinely different strategy. If fewer
than PATH_COUNT genuinely distinct strategies actually exist for this
problem, generate only as many as are real and say so explicitly rather
than padding with artificial variants. For each path, state explicitly:
- Core approach (2-4 sentences)
- What it optimizes for
- What it deliberately sacrifices or is weak against
- A second-order consequence: something that follows from choosing this
  path but isn't obvious from the pitch above
- The one-line condition: what would have to be true about the
  requirements or environment for this to be the correct call
Label them PATH A, PATH B, PATH C.

=== STAGE 2: CROSS-EVALUATION ===
Only now, with all paths fully written, score each against CRITERIA in a
table. For each path, identify the specific scenario or input where it
fails or performs worst — not a generic weakness, an actual concrete
failure case. Do not let any path score well on every criterion by
default; if one genuinely dominates on all axes, say so plainly rather than
manufacturing artificial balance.

=== STAGE 3: SYNTHESIS ===
Either:
(a) select a single winning path and justify it against the runner-up
    directly (why it beats the specific alternative, not just "it's good"), or
(b) construct a hybrid, explicitly labeling which element came from which
    path and why combining them doesn't reintroduce the weakness either
    path had alone.
State which of (a) or (b) you chose and why. Then name which single
criterion, if weighted more heavily, would flip the outcome to a different
path — this is the one thing worth double-checking before committing.

=== STAGE 4: NEXT ===
End with one short line: the concrete failure case found for the winning
(or hybrid) approach in Stage 2, and whether it's worth a full-depth pass
on that specific weak point before committing. One sentence, no more.

TOPIC (problem, design, or decision — leave blank to use this conversation):
```

### Usage
Adjust `PATH_COUNT` or `CRITERIA` if needed, then paste a topic at the very end or leave it blank. Best used before committing to an approach — architecture decisions, competing strategies, anything where "is this even the right way to do it" is still open. Not useful for problems with only one reasonable approach; Stage 1's requirement that paths differ in strategy will surface that quickly rather than manufacturing artificial alternatives.

---

## 3. Domain Taxonomy Mapper

### Purpose
Produces a fixed-shape structural map of a domain — 9 chapters, 9 phases per chapter — instead of prose. Meant as a starting outline to hand off to a separate expansion tool, not a deep-dive itself, so it deliberately stops at two levels deep. Because a topic can be read as belonging to more than one domain, it also proposes up to 3 alternative framings and lets you redirect it before committing to a full expansion elsewhere.

### What was added for rigor
- **MECE discipline.** The tree is only as useful as its structure is sound — chapters that overlap heavily, or that leave an obvious gap between them, defeat the purpose. Added an explicit mutually-exclusive / collectively-exhaustive check rather than relying on "9 chapters" alone to imply good structure.
- **Cross-references.** A strict tree hides real dependencies between branches — a phase node in Chapter 3 that actually depends on one in Chapter 7 gets flattened into looking unrelated. Those get called out explicitly instead of lost.
- **Core vs. peripheral marking.** Not all 9 chapters are equally central to the domain. Marking which ones are core versus adjacent tells you where to spend the expansion budget first.

### Prompt block

```
[DOMAIN TAXONOMY MAPPER]

If TOPIC at the end of this prompt is left blank, infer the subject from
the most recent substantive content in this conversation, or from general
context if there's nothing prior to draw on. If TOPIC is filled in, it
always takes priority over anything inferred.

Infer the domain this topic belongs to and use it as the root.

Produce a Unix-style tree, using ├──, └──, and │ for nesting:
- Root: the domain name.
- Exactly 9 chapter nodes (1 through 9), each a major topic or category
  within the domain, directly related to the subject. Keep the chapters
  mutually exclusive (minimal overlap between them) and collectively
  exhaustive (together they should span the domain without an obvious gap)
  — this matters more than hitting exactly 9 for its own sake.
- Each chapter gets exactly 9 phase nodes (e.g. 1.1 through 1.9): natural
  subtopics, steps, or breakdowns of that chapter.
- Do not expand past the phase level — phase nodes are leaves here, not
  starting points for further nesting.
- Keep every node name a concrete noun phrase, not a vague summary — each
  one should be specific enough to use directly as an expansion prompt
  elsewhere without needing to be reworded first.
- Mark each of the 9 chapters as [CORE] or [PERIPHERAL] relative to the
  domain, next to its heading.

After the tree, output four more sections:

CROSS-REFERENCES:
List any phase nodes that meaningfully depend on or overlap with a phase
node in a different chapter (e.g. "3.2 depends on 7.4"). If there are none
worth noting, say so.

COVERAGE CHECK:
One line confirming the 9 chapters collectively span the domain without an
obvious major gap and without significant overlap between them — or naming
the specific gap or overlap directly if one exists.

ALTERNATIVE DOMAIN READINGS:
Suggest up to 3 different ways the domain could reasonably be interpreted,
in case the mapping above misread the intent. One short paragraph each —
an overview of what that alternative framing would cover, not a full tree.
Ask whether to rebuild the tree against one of these, or to adjust the
domain directly based on a correction given in reply.

RECOMMENDED EXPANSION FIELDS:
Suggest fields worth attaching to each phase node when it gets expanded
later elsewhere — e.g. prerequisites, effort estimate, risk level,
dependencies, sources — tailored to what this specific domain actually
needs, not a generic list reused across every topic.

NEXT:
End with one short line naming the single chapter or phase node that looks
most load-bearing or most likely to need correction — the one worth
confirming before expanding the rest. One sentence, no more.

TOPIC (leave blank to use this conversation):
```

### Usage
Paste a topic at the very end, or leave it blank to map whatever's already being discussed. If the domain reading is off, either name which alternative to rebuild against, or just state the correction directly — no trigger phrase needed, it'll regenerate the tree against the corrected framing.

---

## 4. Debate Simulator

### Purpose
For a specific piece of writing, argument, or position you want ground through repeated rounds of scrutiny rather than a single pass — critique, rewrite, critique the rewrite, and so on, at your own pace, until you're satisfied it holds up. It checks against a fixed list of failure categories every round: hand-waving, half-truths, logical errors, omission, softening, glossing, and contradiction.

One deliberate design choice: the critique is instructed to actually check every category rather than skim past it, but not to invent a problem where a genuine check found none — "always check, never assume it's fine" rather than "always must find something." A version that's forced to manufacture a flaw every round eventually starts flagging non-issues just to have something to say, which stops being useful a few rounds in.

### What was added for rigor
- **Preserve-strength pass.** Critique loops have a known failure mode: fixing the flagged problems while accidentally eroding what was already solid, because nothing was ever asked to protect it. Now the round starts by naming what's actually working, so the rewrite doesn't quietly regress it.
- **Severity tagging.** Not every finding deserves equal weight. Each one now gets tagged major or minor, so you can triage rather than treating a missing citation the same as a genuine contradiction.
- **Diminishing-returns signal.** Nothing previously told you when to stop. If a round only turns up minor findings, it now says so directly — a concrete signal that further rounds are likely to be cosmetic rather than substantive.

### Prompt block

```
[DEBATE SIMULATOR — ITERATIVE CRITIQUE LOOP]

This is a critique-and-rewrite exercise on a specific piece of text, not a
persona change. Between rounds, respond to anything else normally. If
RESPONSE at the end of this prompt is left blank, use the most recent prior
response in this conversation. If RESPONSE is filled in, it always takes
priority over anything inferred.

CATEGORIES: hand-waving, half-truths, logical errors, omission, softening,
            glossing, contradiction

=== ROUND 1 ===

WHAT'S SOLID:
Before critiquing, name what's actually correct and well-supported in the
subject, in one or two lines. This is what the rewrite must not lose or
water down while fixing everything else.

CRITIQUE:
Check the subject against every category in CATEGORIES individually —
don't skip any and don't assume a category is clean without actually
checking it. For each category where you find a real issue, quote the
exact phrase, name the category, tag it MAJOR or MINOR, and explain the
problem plainly. For each category with no real issue after checking,
state "checked, no issue" rather than skipping it silently or inventing
one to fill space. If the same underlying issue keeps surfacing across
categories, say that directly instead of restating it under multiple
headings. If every finding this round is MINOR, say plainly that this is
likely diminishing returns rather than treating it as equivalent to an
earlier round with major findings.

REWRITE:
Address every issue found and restate the subject in full with fixes made,
without losing anything listed under WHAT'S SOLID. Do not reference
categories that had no issue.

NEXT:
End with one short line naming the category most likely to still have a
soft spot in this rewrite, or the specific claim worth pushing on hardest
next round. One sentence, no more.

=== STOP AND WAIT ===
Do not continue automatically. When the user pushes back, sends "AGAIN", or
otherwise indicates they're not satisfied, run another CRITIQUE round on
the latest REWRITE, treating all prior rounds as fair game for reintroduced
or previously missed problems. If a round genuinely finds the same issue
recurring for the second time in the same form, say so explicitly rather
than re-explaining it from scratch. Stop when the user indicates they're
satisfied.

RESPONSE (argument, explanation, or position to critique — leave blank to
use this conversation):
```

### Usage
Paste the text to critique at the very end, or leave it blank to target whatever was just said in the conversation. Get one critique/rewrite round back. Push back, ask a follow-up, or say "again" for another round on the latest version — there's no fixed round limit, it's driven by whether you're satisfied with where it's landed, and the diminishing-returns line will tell you when further rounds are likely a waste of a turn.

---

## When to use which
Deciding between approaches — run **Divergent Path Synthesis** first. Mapping out a domain before diving into any one part of it — run the **Domain Taxonomy Mapper**. Examining a single existing claim, plan, or argument once — run **Full-Depth Topic Analysis** on it. Grinding a specific piece of writing through several rounds until it holds up under real scrutiny — run the **Debate Simulator**.
