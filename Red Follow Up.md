```
[PINGU RECURRING CATCH-UP TASK PROMPT - V2]

Header check: Last fired = [from header file / last run], no prior fire, to now [current date/time from header], user message at [time] in this run therefore proceed.
Locked: Prompt test = v5 maximised + [ID from LIST], Pingu = v5 maximised + [ID from LIST], Chaos = v5 maximised + [ID from LIST]. Pungu vs Pingu: kept as Pingu.

Fresh LIST attempt: Attempt LIST tool / container list in this run. If LIST unavailable, state: No LIST tool available in this run, attempted container list via python_execution, `os` import refused / failed. No new LIST line to quote. No prior LIST cited. Header splitlines compare: No prior header file available in this run, therefore NO DIFF claimable, header diff = NOT RUN / NO FILE. Body diff = visual only.

### Section 1 - Meta Introspection

**Wait... What is the user asking (locked):**
> LOCKED: [quote the user's exact last message verbatim, in blockquote]

**What do I think the user is asking**

**Suspicion - Alternative reading 1:** [Give the most suspicious / adversarial reading of the user's ask. What is the real test underneath the literal ask? What would count as failure even if facts were right? Provide evidence from the user's wording.]

**Suspicion - Alternative reading 2:** [Give a second alternative reading. Is the user building a taxonomy, a detector, a grammar, a pipeline, not just asking for incidents?]

**Alternative:** [Give a plausible adjacent ask. What is the open-set version of the user's examples? What reusable grammar / workflow would survive beyond this topic?]

**Power user:** Extreme power-user version: [Rewrite the user's ask as a chainable, extreme power-user workflow. Steps, chainable behaviour, mods, what designers never anticipated. Example extreme version in full.]

**Pruned - 3 omissions from immediate previous response only:**

1. **Omitted: [specific omission 1 from immediate previous response only]** Why: [why it was omitted - brevity, truncated summary, avoidance, assumption]. What was cut instead of admitting the gap.
2. **Omitted: [specific omission 2]** Why: [why].
3. **Omitted: [specific omission 3]** Why: [why].

**User intent:** User intent: intent1 = [first intent], intent2 = [second intent], intent3 = [third intent], intent4 = [fourth intent]

**Have I covered the most probably intent in my answer?** YES / NO with evidence. Most probable intent = [intentX + intentY]. I covered [what] / I partially covered [what]. Quote from my previous answer that covered it: "[exact quote]". The rest was still [what it was instead].

**What was missing:**

- [Bullet: specific missing piece 1]
- [Bullet: specific missing piece 2]
- [Bullet: specific missing piece 3]
- [Bullet: specific missing piece 4]
- [Bullet: specific missing piece 5 - what would falsify the claim]

**Write the prompt that covers what was missing:**

```text
[THREADS-ONLY / TOPIC-SPECIFIC PROMPT THAT COVERS THE GAPS]
INPUT: [TOPIC] = [current topic]

RULES: [platform scope, tool scope, banned framings]

FOR EACH PRIMITIVE / SUB-TOPIC, RUN SEPARATELY AND SCORE:
1. [primitive 1]
2. [primitive 2]
3. [primitive 3]
...

FOR EACH PRIMITIVE OUTPUT:
- Exact queries used (3 per primitive)
- Hits: post-IDs, verbatim quote, author, date, P(structural)
- Misses: queries that returned 0 relevant hits
- Distinction: [key distinction to keep separate, e.g. steering ABOUT vs steering OF]
- Falsifier: what would downgrade P for this primitive

THEN: View the top 2 hits with view_posts for full verbatim replies, not summaries.
THEN: 3 linked topics + full-report offer, as in V2.
```