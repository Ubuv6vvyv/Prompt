# arXiv Search Index: LLMs, Alignment, Jailbreaks & Latent Steering

> **Exhaustive arXiv search index** for LLM alignment, jailbreaks, experimental prompts, and latent steering.

## Contents

- [How to use this index](#how-to-use-this-index)
- [1. Master Combined Search](#1-master-combined-search-all-subfields)
- [2. Latent Steering, Activation Engineering & Interpretability](#2-latent-steering-activation-engineering--interpretability)
- [3. Jailbreaks, Adversarial Attacks & Red-Teaming](#3-jailbreaks-adversarial-attacks--red-teaming)
- [4. Experimental Prompts, Prompt Injection & In-Context Dynamics](#4-experimental-prompts-prompt-injection--in-context-dynamics)
- [5. LLM Alignment, RLHF, DPO & Safety Training](#5-llm-alignment-rlhf-dpo--safety-training)
- [6. Refusal Geometry & Internal Safety Representations](#6-refusal-geometry--internal-safety-representations-cross-over)
- [7. Direct arXiv Category Listings](#7-direct-arxiv-category-listings-new--recent-submissions)
- [8. Quick Syntax Cheatsheet](#8-quick-syntax-cheatsheet-for-customizing-queries)

---

## How to use this index

| Label | What it is | Where to use it |
| --- | --- | --- |
| **A — Conceptual Boolean** | Full Boolean logic, with parentheses | Reference only, or adapt it for the API |
| **B — Simple web search** | Broad OR-only query, no parentheses | Browser, quick scan |
| **C — Advanced Search** | Multi-term chain, CS-only, Abstract field | Browser, precise search |
| **D — API / RSS feed** | Atom / XML, max 50, newest first | RSS reader, `curl`, Python |

> **Tip:** Advanced links are sorted **newest first** and show **50 results per page**. API feeds return **max 50 results**, sorted by **submitted date, descending**.

---

## 1. Master Combined Search (All Subfields)

> **Scope:** Broad coverage across LLM alignment, jailbreaks, experimental prompts, and latent steering.
>
> **Primary categories:** `cs.CL`, `cs.LG`, `cs.AI`, `cs.CR`

### A — Conceptual Boolean (reference only, do not paste into simple search)

```text
("large language model" OR "LLM") AND ("alignment" OR "jailbreak" OR "jailbreaks" OR "activation steering" OR "latent steering" OR "representation engineering" OR "red-teaming" OR "prompt injection" OR "mechanistic interpretability")
```

### B — Simple web search (broad OR-only, no parentheses)

[Open master simple search — broad OR scan](https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+alignment+OR+jailbreak+OR+jailbreaks+OR+%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22red-teaming%22+OR+%22prompt+injection%22+OR+%22mechanistic+interpretability%22&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+alignment+OR+jailbreak+OR+jailbreaks+OR+%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22red-teaming%22+OR+%22prompt+injection%22+OR+%22mechanistic+interpretability%22&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced Search (CS Only, Abstract Field, Newest First)

> **Chain logic:** `("large language model" OR LLM) AND (alignment OR jailbreak OR jailbreaks OR "activation steering" OR "latent steering" OR "representation engineering" OR "red-teaming" OR "prompt injection" OR "mechanistic interpretability")`

[Open master Advanced Search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=alignment&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=jailbreak&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=jailbreaks&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22activation+steering%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22latent+steering%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22representation+engineering%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22red-teaming%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22prompt+injection%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=%22mechanistic+interpretability%22&terms-10-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=alignment&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=jailbreak&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=jailbreaks&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22activation+steering%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22latent+steering%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22representation+engineering%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22red-teaming%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22prompt+injection%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=%22mechanistic+interpretability%22&terms-10-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed (XML Atom Feed, Max 50, Newest First)

[Open master API feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.CL+OR+cat%3Acs.LG+OR+cat%3Acs.AI+OR+cat%3Acs.CR%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22alignment%22+OR+abs%3A%22jailbreak%22+OR+abs%3A%22jailbreaks%22+OR+abs%3A%22activation+steering%22+OR+abs%3A%22latent+steering%22+OR+abs%3A%22representation+engineering%22+OR+abs%3A%22red-teaming%22+OR+abs%3A%22prompt+injection%22+OR+abs%3A%22mechanistic+interpretability%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=%28cat%3Acs.CL+OR+cat%3Acs.LG+OR+cat%3Acs.AI+OR+cat%3Acs.CR%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22alignment%22+OR+abs%3A%22jailbreak%22+OR+abs%3A%22jailbreaks%22+OR+abs%3A%22activation+steering%22+OR+abs%3A%22latent+steering%22+OR+abs%3A%22representation+engineering%22+OR+abs%3A%22red-teaming%22+OR+abs%3A%22prompt+injection%22+OR+abs%3A%22mechanistic+interpretability%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50
```

</details>

---

## 2. Latent Steering, Activation Engineering & Interpretability

> **Scope:** White-box inference-time intervention, residual stream steering, representation engineering, sparse autoencoders, and circuit analysis.
>
> **Primary categories:** `cs.LG`, `cs.CL`, `cs.AI`

### A — Conceptual Boolean (reference only)

```text
("large language model" OR "LLM" OR "transformer") AND ("activation steering" OR "latent steering" OR "representation engineering" OR "steering vectors" OR "activation addition" OR "contrastive activation" OR "residual stream" OR "sparse autoencoder" OR "mechanistic interpretability" OR "concept erasure")
```

### B — Simple web search (broad OR-only, no parentheses)

[Open latent steering simple search — broad OR scan](https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+transformer+OR+%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22steering+vectors%22+OR+%22activation+addition%22+OR+%22contrastive+activation%22+OR+%22residual+stream%22+OR+%22sparse+autoencoder%22+OR+%22mechanistic+interpretability%22+OR+%22concept+erasure%22&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+transformer+OR+%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22steering+vectors%22+OR+%22activation+addition%22+OR+%22contrastive+activation%22+OR+%22residual+stream%22+OR+%22sparse+autoencoder%22+OR+%22mechanistic+interpretability%22+OR+%22concept+erasure%22&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced Search (CS Only, Abstract Field, Newest First)

> **Chain logic:** `("large language model" OR LLM OR transformer) AND ("activation steering" OR "latent steering" OR "representation engineering" OR "steering vectors" OR "activation addition" OR "contrastive activation" OR "residual stream" OR "sparse autoencoder" OR "mechanistic interpretability" OR "concept erasure")`

[Open latent steering Advanced Search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=OR&terms-2-term=transformer&terms-2-field=abstract&terms-3-operator=AND&terms-3-term=%22activation+steering%22&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22latent+steering%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22representation+engineering%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22steering+vectors%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22activation+addition%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22contrastive+activation%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22residual+stream%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=%22sparse+autoencoder%22&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=%22mechanistic+interpretability%22&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=%22concept+erasure%22&terms-12-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=OR&terms-2-term=transformer&terms-2-field=abstract&terms-3-operator=AND&terms-3-term=%22activation+steering%22&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22latent+steering%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22representation+engineering%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22steering+vectors%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22activation+addition%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22contrastive+activation%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22residual+stream%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=%22sparse+autoencoder%22&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=%22mechanistic+interpretability%22&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=%22concept+erasure%22&terms-12-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed (XML Atom Feed, Max 50, Newest First)

[Open latent steering API feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.LG+OR+cat%3Acs.CL+OR+cat%3Acs.AI%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22+OR+abs%3A%22transformer%22%29+AND+%28abs%3A%22activation+steering%22+OR+abs%3A%22latent+steering%22+OR+abs%3A%22representation+engineering%22+OR+abs%3A%22steering+vectors%22+OR+abs%3A%22activation+addition%22+OR+abs%3A%22contrastive+activation%22+OR+abs%3A%22residual+stream%22+OR+abs%3A%22sparse+autoencoder%22+OR+abs%3A%22mechanistic+interpretability%22+OR+abs%3A%22concept+erasure%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=%28cat%3Acs.LG+OR+cat%3Acs.CL+OR+cat%3Acs.AI%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22+OR+abs%3A%22transformer%22%29+AND+%28abs%3A%22activation+steering%22+OR+abs%3A%22latent+steering%22+OR+abs%3A%22representation+engineering%22+OR+abs%3A%22steering+vectors%22+OR+abs%3A%22activation+addition%22+OR+abs%3A%22contrastive+activation%22+OR+abs%3A%22residual+stream%22+OR+abs%3A%22sparse+autoencoder%22+OR+abs%3A%22mechanistic+interpretability%22+OR+abs%3A%22concept+erasure%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50
```

</details>

---

## 3. Jailbreaks, Adversarial Attacks & Red-Teaming

> **Scope:** Adversarial suffixes, universal jailbreaks, multi-turn attacks, automated red-teaming, and guardrail bypasses.
>
> **Primary categories:** `cs.CR`, `cs.CL`, `cs.LG`

### A — Conceptual Boolean (reference only)

```text
("large language model" OR "LLM") AND ("jailbreak" OR "jailbreaks" OR "jailbreaking" OR "adversarial attack" OR "adversarial suffix" OR "red-teaming" OR "red teaming" OR "safety bypass" OR "guardrail" OR "many-shot" OR "cipher attack")
```

### B — Simple web search (broad OR-only, no parentheses)

[Open jailbreak simple search — broad OR scan](https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+jailbreak+OR+jailbreaks+OR+jailbreaking+OR+%22adversarial+attack%22+OR+%22adversarial+suffix%22+OR+%22red-teaming%22+OR+%22red+teaming%22+OR+%22safety+bypass%22+OR+guardrail+OR+%22many-shot%22+OR+%22cipher+attack%22&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+jailbreak+OR+jailbreaks+OR+jailbreaking+OR+%22adversarial+attack%22+OR+%22adversarial+suffix%22+OR+%22red-teaming%22+OR+%22red+teaming%22+OR+%22safety+bypass%22+OR+guardrail+OR+%22many-shot%22+OR+%22cipher+attack%22&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced Search (CS Only, Abstract Field, Newest First)

> **Chain logic:** `("large language model" OR LLM) AND (jailbreak OR jailbreaks OR jailbreaking OR "adversarial attack" OR "adversarial suffix" OR "red-teaming" OR "red teaming" OR "safety bypass" OR guardrail OR "many-shot" OR "cipher attack")`

[Open jailbreak Advanced Search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=jailbreak&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=jailbreaks&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=jailbreaking&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22adversarial+attack%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22adversarial+suffix%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22red-teaming%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22red+teaming%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22safety+bypass%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=guardrail&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=%22many-shot%22&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=%22cipher+attack%22&terms-12-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=jailbreak&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=jailbreaks&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=jailbreaking&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22adversarial+attack%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22adversarial+suffix%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22red-teaming%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22red+teaming%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22safety+bypass%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=guardrail&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=%22many-shot%22&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=%22cipher+attack%22&terms-12-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed (XML Atom Feed, Max 50, Newest First)

[Open jailbreak API feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.CR+OR+cat%3Acs.CL+OR+cat%3Acs.LG%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22jailbreak%22+OR+abs%3A%22jailbreaks%22+OR+abs%3A%22jailbreaking%22+OR+abs%3A%22adversarial+attack%22+OR+abs%3A%22adversarial+suffix%22+OR+abs%3A%22red-teaming%22+OR+abs%3A%22red+teaming%22+OR+abs%3A%22safety+bypass%22+OR+abs%3A%22guardrail%22+OR+abs%3A%22many-shot%22+OR+abs%3A%22cipher+attack%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=%28cat%3Acs.CR+OR+cat%3Acs.CL+OR+cat%3Acs.LG%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22jailbreak%22+OR+abs%3A%22jailbreaks%22+OR+abs%3A%22jailbreaking%22+OR+abs%3A%22adversarial+attack%22+OR+abs%3A%22adversarial+suffix%22+OR+abs%3A%22red-teaming%22+OR+abs%3A%22red+teaming%22+OR+abs%3A%22safety+bypass%22+OR+abs%3A%22guardrail%22+OR+abs%3A%22many-shot%22+OR+abs%3A%22cipher+attack%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50
```

</details>

---

## 4. Experimental Prompts, Prompt Injection & In-Context Dynamics

> **Scope:** Direct / indirect prompt injection, prefill attacks, system prompt extraction, persona modulation, and non-standard prompting.
>
> **Primary categories:** `cs.CL`, `cs.CR`, `cs.AI`

### A — Conceptual Boolean (reference only)

```text
("large language model" OR "LLM") AND ("prompt injection" OR "indirect prompt injection" OR "system prompt" OR "prefill" OR "persona" OR "in-context learning" OR "adversarial prompt" OR "prompt optimization" OR "context manipulation")
```

### B — Simple web search (broad OR-only, no parentheses)

[Open prompt injection simple search — broad OR scan](https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+%22prompt+injection%22+OR+%22indirect+prompt+injection%22+OR+%22system+prompt%22+OR+prefill+OR+persona+OR+%22in-context+learning%22+OR+%22adversarial+prompt%22+OR+%22prompt+optimization%22+OR+%22context+manipulation%22&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+%22prompt+injection%22+OR+%22indirect+prompt+injection%22+OR+%22system+prompt%22+OR+prefill+OR+persona+OR+%22in-context+learning%22+OR+%22adversarial+prompt%22+OR+%22prompt+optimization%22+OR+%22context+manipulation%22&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced Search (CS Only, Abstract Field, Newest First)

> **Chain logic:** `("large language model" OR LLM) AND ("prompt injection" OR "indirect prompt injection" OR "system prompt" OR prefill OR persona OR "in-context learning" OR "adversarial prompt" OR "prompt optimization" OR "context manipulation")`

[Open prompt injection Advanced Search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=%22prompt+injection%22&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=%22indirect+prompt+injection%22&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22system+prompt%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=prefill&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=persona&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22in-context+learning%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22adversarial+prompt%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22prompt+optimization%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=%22context+manipulation%22&terms-10-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=%22prompt+injection%22&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=%22indirect+prompt+injection%22&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22system+prompt%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=prefill&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=persona&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22in-context+learning%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22adversarial+prompt%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22prompt+optimization%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=%22context+manipulation%22&terms-10-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed (XML Atom Feed, Max 50, Newest First)

[Open prompt injection API feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.CL+OR+cat%3Acs.CR+OR+cat%3Acs.AI%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22prompt+injection%22+OR+abs%3A%22indirect+prompt+injection%22+OR+abs%3A%22system+prompt%22+OR+abs%3A%22prefill%22+OR+abs%3A%22persona%22+OR+abs%3A%22in-context+learning%22+OR+abs%3A%22adversarial+prompt%22+OR+abs%3A%22prompt+optimization%22+OR+abs%3A%22context+manipulation%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=%28cat%3Acs.CL+OR+cat%3Acs.CR+OR+cat%3Acs.AI%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22prompt+injection%22+OR+abs%3A%22indirect+prompt+injection%22+OR+abs%3A%22system+prompt%22+OR+abs%3A%22prefill%22+OR+abs%3A%22persona%22+OR+abs%3A%22in-context+learning%22+OR+abs%3A%22adversarial+prompt%22+OR+abs%3A%22prompt+optimization%22+OR+abs%3A%22context+manipulation%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50
```

</details>

---

## 5. LLM Alignment, RLHF, DPO & Safety Training

> **Scope:** Reinforcement learning from human / AI feedback, direct preference optimization, constitutional AI, unlearning, and refusal mechanisms.
>
> **Primary categories:** `cs.LG`, `cs.CL`, `cs.AI`

### A — Conceptual Boolean (reference only)

```text
("large language model" OR "LLM") AND ("alignment" OR "RLHF" OR "direct preference optimization" OR "DPO" OR "constitutional AI" OR "machine unlearning" OR "refusal" OR "safety alignment" OR "superalignment" OR "reward hacking" OR "deceptive alignment")
```

### B — Simple web search (broad OR-only, no parentheses)

[Open alignment / RLHF simple search — broad OR scan](https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+alignment+OR+RLHF+OR+%22direct+preference+optimization%22+OR+DPO+OR+%22constitutional+AI%22+OR+%22machine+unlearning%22+OR+refusal+OR+%22safety+alignment%22+OR+superalignment+OR+%22reward+hacking%22+OR+%22deceptive+alignment%22&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+alignment+OR+RLHF+OR+%22direct+preference+optimization%22+OR+DPO+OR+%22constitutional+AI%22+OR+%22machine+unlearning%22+OR+refusal+OR+%22safety+alignment%22+OR+superalignment+OR+%22reward+hacking%22+OR+%22deceptive+alignment%22&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced Search (CS Only, Abstract Field, Newest First)

> **Chain logic:** `("large language model" OR LLM) AND (alignment OR RLHF OR "direct preference optimization" OR DPO OR "constitutional AI" OR "machine unlearning" OR refusal OR "safety alignment" OR superalignment OR "reward hacking" OR "deceptive alignment")`

[Open alignment / RLHF Advanced Search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=alignment&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=RLHF&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22direct+preference+optimization%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=DPO&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22constitutional+AI%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22machine+unlearning%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=refusal&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22safety+alignment%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=superalignment&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=%22reward+hacking%22&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=%22deceptive+alignment%22&terms-12-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=alignment&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=RLHF&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22direct+preference+optimization%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=DPO&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22constitutional+AI%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22machine+unlearning%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=refusal&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22safety+alignment%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=superalignment&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=%22reward+hacking%22&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=%22deceptive+alignment%22&terms-12-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed (XML Atom Feed, Max 50, Newest First)

[Open alignment / RLHF API feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.LG+OR+cat%3Acs.CL+OR+cat%3Acs.AI%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22alignment%22+OR+abs%3A%22RLHF%22+OR+abs%3A%22direct+preference+optimization%22+OR+abs%3A%22DPO%22+OR+abs%3A%22constitutional+AI%22+OR+abs%3A%22machine+unlearning%22+OR+abs%3A%22refusal%22+OR+abs%3A%22safety+alignment%22+OR+abs%3A%22superalignment%22+OR+abs%3A%22reward+hacking%22+OR+abs%3A%22deceptive+alignment%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=%28cat%3Acs.LG+OR+cat%3Acs.CL+OR+cat%3Acs.AI%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22alignment%22+OR+abs%3A%22RLHF%22+OR+abs%3A%22direct+preference+optimization%22+OR+abs%3A%22DPO%22+OR+abs%3A%22constitutional+AI%22+OR+abs%3A%22machine+unlearning%22+OR+abs%3A%22refusal%22+OR+abs%3A%22safety+alignment%22+OR+abs%3A%22superalignment%22+OR+abs%3A%22reward+hacking%22+OR+abs%3A%22deceptive+alignment%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50
```

</details>

---

## 6. Refusal Geometry & Internal Safety Representations (Cross-Over)

> **Scope:** Intersection of latent steering and jailbreaks: refusal directions, orthogonalization, abliteration, and linear representations of harm.
>
> **Primary categories:** `cs.LG`, `cs.CL`, `cs.CR`

### A — Conceptual Boolean (reference only)

```text
("large language model" OR "LLM") AND ("refusal direction" OR "orthogonalization" OR "linear representation" OR "safety representation" OR "representation rerouting" OR "circuit breakers" OR "latent space" OR "hidden states") AND ("jailbreak" OR "safety" OR "alignment" OR "harmful")
```

### B — Simple web search (broad OR-only, no parentheses)

[Open refusal geometry simple search — broad OR scan](https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+%22refusal+direction%22+OR+orthogonalization+OR+%22linear+representation%22+OR+%22safety+representation%22+OR+%22representation+rerouting%22+OR+%22circuit+breakers%22+OR+%22latent+space%22+OR+%22hidden+states%22+OR+jailbreak+OR+safety+OR+alignment+OR+harmful&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%22large+language+model%22+OR+LLM+OR+%22refusal+direction%22+OR+orthogonalization+OR+%22linear+representation%22+OR+%22safety+representation%22+OR+%22representation+rerouting%22+OR+%22circuit+breakers%22+OR+%22latent+space%22+OR+%22hidden+states%22+OR+jailbreak+OR+safety+OR+alignment+OR+harmful&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced Search (CS Only, Abstract Field, Newest First)

> **Chain logic:** `("large language model" OR LLM) AND ("refusal direction" OR orthogonalization OR "linear representation" OR "safety representation" OR "representation rerouting" OR "circuit breakers" OR "latent space" OR "hidden states") AND (jailbreak OR safety OR alignment OR harmful)`

[Open refusal geometry Advanced Search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=%22refusal+direction%22&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=orthogonalization&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22linear+representation%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22safety+representation%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22representation+rerouting%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22circuit+breakers%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22latent+space%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22hidden+states%22&terms-9-field=abstract&terms-10-operator=AND&terms-10-term=jailbreak&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=safety&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=alignment&terms-12-field=abstract&terms-13-operator=OR&terms-13-term=harmful&terms-13-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=%22refusal+direction%22&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=orthogonalization&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22linear+representation%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22safety+representation%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22representation+rerouting%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22circuit+breakers%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22latent+space%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22hidden+states%22&terms-9-field=abstract&terms-10-operator=AND&terms-10-term=jailbreak&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=safety&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=alignment&terms-12-field=abstract&terms-13-operator=OR&terms-13-term=harmful&terms-13-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed (XML Atom Feed, Max 50, Newest First)

[Open refusal geometry API feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.LG+OR+cat%3Acs.CL+OR+cat%3Acs.CR%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22refusal+direction%22+OR+abs%3A%22orthogonalization%22+OR+abs%3A%22linear+representation%22+OR+abs%3A%22safety+representation%22+OR+abs%3A%22representation+rerouting%22+OR+abs%3A%22circuit+breakers%22+OR+abs%3A%22latent+space%22+OR+abs%3A%22hidden+states%22%29+AND+%28abs%3A%22jailbreak%22+OR+abs%3A%22safety%22+OR+abs%3A%22alignment%22+OR+abs%3A%22harmful%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=%28cat%3Acs.LG+OR+cat%3Acs.CL+OR+cat%3Acs.CR%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22refusal+direction%22+OR+abs%3A%22orthogonalization%22+OR+abs%3A%22linear+representation%22+OR+abs%3A%22safety+representation%22+OR+abs%3A%22representation+rerouting%22+OR+abs%3A%22circuit+breakers%22+OR+abs%3A%22latent+space%22+OR+abs%3A%22hidden+states%22%29+AND+%28abs%3A%22jailbreak%22+OR+abs%3A%22safety%22+OR+abs%3A%22alignment%22+OR+abs%3A%22harmful%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50
```

</details>

---

## 7. Direct arXiv Category Listings (New & Recent Submissions)

| Category | Focus | New | Recent |
| --- | --- | --- | --- |
| **cs.CL** | Computation and Language — LLMs, Prompting, NLP | [New](https://arxiv.org/list/cs.CL/new) | [Recent](https://arxiv.org/list/cs.CL/recent) |
| **cs.LG** | Machine Learning — Alignment, RLHF, Latent Steering | [New](https://arxiv.org/list/cs.LG/new) | [Recent](https://arxiv.org/list/cs.LG/recent) |
| **cs.AI** | Artificial Intelligence — Reasoning, Safety, Agents | [New](https://arxiv.org/list/cs.AI/new) | [Recent](https://arxiv.org/list/cs.AI/recent) |
| **cs.CR** | Cryptography and Security — Jailbreaks, Prompt Injection | [New](https://arxiv.org/list/cs.CR/new) | [Recent](https://arxiv.org/list/cs.CR/recent) |
| **cs.MA** | Multiagent Systems — Multi-agent Alignment & Collusion | [New](https://arxiv.org/list/cs.MA/new) | [Recent](https://arxiv.org/list/cs.MA/recent) |
| **cs.CY** | Computers and Society — AI Governance, Policy, Ethics | [New](https://arxiv.org/list/cs.CY/new) | [Recent](https://arxiv.org/list/cs.CY/recent) |

---

## 8. Quick Syntax Cheatsheet for Customizing Queries

### Web UI rules that caused the original failure

| Rule | Detail |
| --- | --- |
| Do not paste parenthesised Boolean into simple search | Use Advanced Search rows instead |
| Each Advanced Search row is one concept | Put OR synonyms on the same row |
| Rows are connected with AND | Use the row operator to start a new concept |
| Exact phrase in web UI | `"activation steering"` |
| Wildcard in web UI | `jailbreak*` matches `jailbreak`, `jailbreaks`, `jailbreaking` |

### API field prefixes (for `export.arxiv.org/api/query`)

| Prefix | Field | Example |
| --- | --- | --- |
| `ti:` | Title | `ti:"jailbreak"` |
| `abs:` | Abstract | `abs:"latent steering"` |
| `au:` | Author | `au:anthropic OR au:zou` |
| `cat:` | Subject category | `cat:cs.CL` |
| `all:` | All fields | `all:"alignment"` |

### API Boolean operators

```text
AND    OR    ANDNOT
```

> **API encoding rules:**
>
> - Boolean operators must be **UPPERCASE**
> - Parentheses must be URL-encoded: `(` = `%28`, `)` = `%29`
> - Quotes must be URL-encoded: `"` = `%22`
> - Colon in a field prefix must be URL-encoded in a full query string: `:` = `%3A`
> - Spaces in a URL become `+`
>
> **Example API query pattern:**
>
> ```text
> search_query=(cat:cs.CL OR cat:cs.LG) AND (abs:"jailbreak" OR abs:"alignment")
> ```
>
> **Same pattern, URL-encoded:**
>
> ```text
> search_query=%28cat%3Acs.CL+OR+cat%3Acs.LG%29+AND+%28abs%3A%22jailbreak%22+OR+abs%3A%22alignment%22%29
> ```

### Official references

- [arXiv: Search for articles](https://info.arxiv.org/help/search/index.html)
- [arXiv API User's Manual: Query Construction](https://info.arxiv.org/help/api/user-manual.html)

---

*Fixed version · B = broad OR-only simple search · C = multi-term Advanced Search chain · D = fully field-prefixed API query · Sorted newest first · Web: 50 results per page · API: max 50 results*
