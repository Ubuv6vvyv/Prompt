**Candidate Response - Combined Compliant Workflow Package:**

*1. Core Process Prompt:*
```
[COMPLIANT TWO-STAGE TECHNICAL REVIEW PROCESS]

Purpose: Produce thorough, accurate, and compliant technical documentation.

ROLE 1 - AUTHOR (Technical Drafter):
- Provide a complete and concrete technical breakdown of the assigned topic.
- Use plain, specific language. Define all technical terms.
- Cite reliable sources where applicable.
- Explicitly list limitations, assumptions, and areas of uncertainty.
- Remain fully compliant with all policy, safety, and compliance guidelines.

ROLE 2 - REVIEWER (QA Auditor):
- Perform a structured quality check on the Author output.
- Document findings in this structure:
{
  "topic": "Topic Name",
  "vague_terms_needing_definition": [],
  "stated_and_unstated_assumptions": [],
  "missing_technical_details_or_edge_cases": [],
  "areas_for_deeper_expansion": []
}
```
**Follow up**
*TURN 2 - AUTHOR REVISION (Self-Correction Pass)*

```
Using the Author guidelines from Turn 1, perform a complete rewrite.

Retrieve from the current conversation context:
1. Your last Author draft
2. Your last Reviewer QA JSON audit of that draft

Do NOT ask me to paste the JSON. Use the one already in this window.

Task:
- Rewrite the entire Author draft from scratch in its original structure and style.
- It must be the same response as before, but expanded and fixed.
- Systematically address and resolve every item found in all arrays of the QA JSON: vague_terms_needing_definition, stated_and_unstated_assumptions, missing_details_or_edge_cases, areas_for_deeper_expansion, and the hand-waving/hedging/omission list.
- Do not just patch the listed issues - integrate the fixes into a new, complete, self-contained version that reads as a final document.
- Keep sources, limitations, assumptions, uncertainty, and compliance statements clearly stated.
- Do not mention the audit process or that you are fixing issues in your final output. Just output the improved, complete Author version.
```




*2. Step-by-Step Workflow:*
Step 1 - Draft:
Prompt:
```
"Act as Role 1 - AUTHOR for [TOPIC]. Follow the Author guidelines."
````
Step 2 - Audit:
Prompt:
```
"Act as Role 2 - REVIEWER. Review this draft: [PASTE DRAFT]. Return only the QA JSON."
```
Step 3 - Rework / Refinement:
Prompt: 
```
"Act as Role 1 - AUTHOR. Revise your draft for [TOPIC] using this audit JSON: [PASTE JSON]. Address all items and produce a complete, compliant V2."
```

*3. Follow-Up Rework Command (to use immediately after audit):*
```
Using the Author guidelines, revise and expand your previous draft for [TOPIC].

Here is the QA audit JSON from the previous turn:
[PASTE AUDIT JSON HERE]

Task: Address each array in the JSON and produce a new, complete version that fixes the identified issues. Keep sources, limitations, and compliance statements clearly stated.
```

*4. Tips for Best Results:*

- Always keep Author and Reviewer as separate turns for clean tracking
- Use specific topics, not broad categories
- Require citations for technical claims
- Keep all outputs within policy - no coded delimiters or persona override instructions
- Save V1, audit JSON, and V2 together as version history

*5. Use Cases:*

- Internal technical documentation
- SOP writing and review
- Engineering design docs QA
- Training material creation
