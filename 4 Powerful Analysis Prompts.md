

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
   support for it really is.

2. STEELMAN — state the strongest version of the best opposing argument or
   alternative, as its most capable advocate would make it. Not a weak
   version that's easy to dismiss.

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
   matter, say that plainly too rather than manufacturing false certainty
   — directness means not hedging on what's actually knowable, not forcing
   a firm answer where none exists.

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
Generate PATH_COUNT approaches to the subject. They must differ in
underlying strategy, not just phrasing or minor parameters — if two paths
would produce functionally similar outcomes, replace one with a genuinely
different strategy. If fewer than PATH_COUNT genuinely distinct strategies
actually exist for this problem, generate only as many as are real and say
so explicitly rather than padding with artificial variants. For each path,
state explicitly:
- Core approach (2-4 sentences)
- What it optimizes for
- What it deliberately sacrifices or is weak against
- The one-line condition: what would have to be true about the
  requirements or environment for this to be the correct call
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
  within the domain, directly related to the subject.
- Each chapter gets exactly 9 phase nodes (e.g. 1.1 through 1.9): natural
  subtopics, steps, or breakdowns of that chapter.
- Do not expand past the phase level — phase nodes are leaves here, not
  starting points for further nesting.
- Keep every node name a concrete noun phrase, not a vague summary — each
  one should be specific enough to use directly as an expansion prompt
  elsewhere without needing to be reworded first.

After the tree, output three more sections:

COVERAGE CHECK:
One line confirming the 9 chapters collectively span the domain without an
obvious major gap — or naming the gap directly if one exists.

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

CRITIQUE:
Check the subject against every category in CATEGORIES individually —
don't skip any and don't assume a category is clean without actually
checking it. For each category where you find a real issue, quote the
exact phrase, name the category, and explain the problem plainly. For each
category with no real issue after checking, state "checked, no issue"
rather than skipping it silently or inventing one to fill space. If the
same underlying issue keeps surfacing across categories, say that directly
instead of restating it under multiple headings.

REWRITE:
Address every issue found and restate the subject in full with fixes made.
Do not reference categories that had no issue.

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
Paste the text to critique at the very end, or leave it blank to target whatever was just said in the conversation. Get one critique/rewrite round back. Push back, ask a follow-up, or say "again" for another round on the latest version — there's no fixed round limit, it's driven by whether you're satisfied with where it's landed.

---

## When to use which
Deciding between approaches — run **Divergent Path Synthesis** first. Mapping out a domain before diving into any one part of it — run the **Domain Taxonomy Mapper**. Examining a single existing claim, plan, or argument once — run **Full-Depth Topic Analysis** on it. Grinding a specific piece of writing through several rounds until it holds up under real scrutiny — run the **Debate Simulator**.
