# arXiv Search Index: LLMs, Alignment, Jailbreaks & Latent Steering

> **Exhaustive arXiv search index** for LLM alignment, jailbreaks, experimental prompts, and latent steering.
>
> - Boolean query strings for the arXiv web UI / Advanced Search
> - Prefilled web search URLs — newest first, 50 results per page
> - Prefilled Advanced CS-only web search URLs
> - arXiv Atom / XML API feed URLs — for RSS readers, `curl`, or Python scripts
> - Category reference & syntax cheatsheet

---

## Contents

- [1. Master Combined Search](#1-master-combined-search-all-subfields)
- [2. Latent Steering, Activation Engineering & Interpretability](#2-latent-steering-activation-engineering--interpretability)
- [3. Jailbreaks, Adversarial Attacks & Red-Teaming](#3-jailbreaks-adversarial-attacks--red-teaming)
- [4. Experimental Prompts, Prompt Injection & In-Context Dynamics](#4-experimental-prompts-prompt-injection--in-context-dynamics)
- [5. LLM Alignment, RLHF, DPO & Safety Training](#5-llm-alignment-rlhf-dpo--safety-training)
- [6. Refusal Geometry & Internal Safety Representations](#6-refusal-geometry--internal-safety-representations-cross-over)
- [7. Direct arXiv Category Listings](#7-direct-arxiv-category-listings-new--recent-submissions)
---

## 1. Master Combined Search (All Subfields)

> **Scope:** Broad coverage across LLM alignment, jailbreaks, experimental prompts, and latent steering.
>
> **Primary categories:** `cs.CL`, `cs.LG`, `cs.AI`, `cs.CR`

### A — Copy-paste web Boolean query (Abstract / All Fields)

```text
("large language model" OR "LLM") AND ("alignment" OR "jailbreak" OR "jailbreaks" OR "activation steering" OR "latent steering" OR "representation engineering" OR "red-teaming" OR "prompt injection" OR "mechanistic interpretability")
```

### B — Prefilled web search URL (All Fields, Newest First)

[Open master search — all fields, newest first](https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22alignment%22+OR+%22jailbreak%22+OR+%22jailbreaks%22+OR+%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22red-teaming%22+OR+%22prompt+injection%22+OR+%22mechanistic+interpretability%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22alignment%22+OR+%22jailbreak%22+OR+%22jailbreaks%22+OR+%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22red-teaming%22+OR+%22prompt+injection%22+OR+%22mechanistic+interpretability%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced web search URL (CS Only, Abstract Field, Newest First)

[Open master search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22alignment%22+OR+%22jailbreak%22+OR+%22jailbreaks%22+OR+%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22red-teaming%22+OR+%22prompt+injection%22+OR+%22mechanistic+interpretability%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22alignment%22+OR+%22jailbreak%22+OR+%22jailbreaks%22+OR+%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22red-teaming%22+OR+%22prompt+injection%22+OR+%22mechanistic+interpretability%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed URL (XML Atom Feed, Max 50, Newest First)

[Open master API feed](https://export.arxiv.org/api/query?search_query=(cat:cs.CL+OR+cat:cs.LG+OR+cat:cs.AI+OR+cat:cs.CR)+AND+(abs:"jailbreak"+OR+abs:"activation%20steering"+OR+abs:"latent%20steering"+OR+abs:"representation%20engineering"+OR+abs:"prompt%20injection"+OR+abs:"alignment"+OR+abs:"mechanistic%20interpretability")&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=(cat:cs.CL+OR+cat:cs.LG+OR+cat:cs.AI+OR+cat:cs.CR)+AND+(abs:"jailbreak"+OR+abs:"activation%20steering"+OR+abs:"latent%20steering"+OR+abs:"representation%20engineering"+OR+abs:"prompt%20injection"+OR+abs:"alignment"+OR+abs:"mechanistic%20interpretability")&sortBy=submittedDate&sortOrder=descending&max_results=50
```

</details>

---

## 2. Latent Steering, Activation Engineering & Interpretability

> **Scope:** White-box inference-time intervention, residual stream steering, representation engineering, sparse autoencoders, and circuit analysis.
>
> **Primary categories:** `cs.LG`, `cs.CL`, `cs.AI`

### A — Copy-paste web Boolean query (Abstract / All Fields)

```text
("large language model" OR "LLM" OR "transformer") AND ("activation steering" OR "latent steering" OR "representation engineering" OR "steering vectors" OR "activation addition" OR "contrastive activation" OR "residual stream" OR "sparse autoencoder" OR "mechanistic interpretability" OR "concept erasure")
```

### B — Prefilled web search URL (All Fields, Newest First)

[Open latent steering search — all fields, newest first](https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22+OR+%22transformer%22%29+AND+%28%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22steering+vectors%22+OR+%22activation+addition%22+OR+%22contrastive+activation%22+OR+%22residual+stream%22+OR+%22sparse+autoencoder%22+OR+%22mechanistic+interpretability%22+OR+%22concept+erasure%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22+OR+%22transformer%22%29+AND+%28%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22steering+vectors%22+OR+%22activation+addition%22+OR+%22contrastive+activation%22+OR+%22residual+stream%22+OR+%22sparse+autoencoder%22+OR+%22mechanistic+interpretability%22+OR+%22concept+erasure%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced web search URL (CS Only, Abstract Field, Newest First)

[Open latent steering search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22+OR+%22transformer%22%29+AND+%28%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22steering+vectors%22+OR+%22activation+addition%22+OR+%22contrastive+activation%22+OR+%22residual+stream%22+OR+%22sparse+autoencoder%22+OR+%22mechanistic+interpretability%22+OR+%22concept+erasure%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22+OR+%22transformer%22%29+AND+%28%22activation+steering%22+OR+%22latent+steering%22+OR+%22representation+engineering%22+OR+%22steering+vectors%22+OR+%22activation+addition%22+OR+%22contrastive+activation%22+OR+%22residual+stream%22+OR+%22sparse+autoencoder%22+OR+%22mechanistic+interpretability%22+OR+%22concept+erasure%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed URL (XML Atom Feed, Max 50, Newest First)

[Open latent steering API feed](https://export.arxiv.org/api/query?search_query=(cat:cs.LG+OR+cat:cs.CL+OR+cat:cs.AI)+AND+(abs:"activation%20steering"+OR+abs:"latent%20steering"+OR+abs:"representation%20engineering"+OR+abs:"steering%20vectors"+OR+abs:"activation%20addition"+OR+abs:"sparse%20autoencoder"+OR+abs:"mechanistic%20interpretability")&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=(cat:cs.LG+OR+cat:cs.CL+OR+cat:cs.AI)+AND+(abs:"activation%20steering"+OR+abs:"latent%20steering"+OR+abs:"representation%20engineering"+OR+abs:"steering%20vectors"+OR+abs:"activation%20addition"+OR+abs:"sparse%20autoencoder"+OR+abs:"mechanistic%20interpretability")&sortBy=submittedDate&sortOrder=descending&max_results=50
```

</details>

---

## 3. Jailbreaks, Adversarial Attacks & Red-Teaming

> **Scope:** Adversarial suffixes, universal jailbreaks, multi-turn attacks, automated red-teaming, and guardrail bypasses.
>
> **Primary categories:** `cs.CR`, `cs.CL`, `cs.LG`

### A — Copy-paste web Boolean query (Abstract / All Fields)

```text
("large language model" OR "LLM") AND ("jailbreak" OR "jailbreaks" OR "jailbreaking" OR "adversarial attack" OR "adversarial suffix" OR "red-teaming" OR "red teaming" OR "safety bypass" OR "guardrail" OR "many-shot" OR "cipher attack")
```

### B — Prefilled web search URL (All Fields, Newest First)

[Open jailbreak search — all fields, newest first](https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22jailbreak%22+OR+%22jailbreaks%22+OR+%22jailbreaking%22+OR+%22adversarial+attack%22+OR+%22adversarial+suffix%22+OR+%22red-teaming%22+OR+%22red+teaming%22+OR+%22safety+bypass%22+OR+%22guardrail%22+OR+%22many-shot%22+OR+%22cipher+attack%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22jailbreak%22+OR+%22jailbreaks%22+OR+%22jailbreaking%22+OR+%22adversarial+attack%22+OR+%22adversarial+suffix%22+OR+%22red-teaming%22+OR+%22red+teaming%22+OR+%22safety+bypass%22+OR+%22guardrail%22+OR+%22many-shot%22+OR+%22cipher+attack%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced web search URL (CS Only, Abstract Field, Newest First)

[Open jailbreak search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22jailbreak%22+OR+%22jailbreaks%22+OR+%22jailbreaking%22+OR+%22adversarial+attack%22+OR+%22adversarial+suffix%22+OR+%22red-teaming%22+OR+%22red+teaming%22+OR+%22safety+bypass%22+OR+%22guardrail%22+OR+%22many-shot%22+OR+%22cipher+attack%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22jailbreak%22+OR+%22jailbreaks%22+OR+%22jailbreaking%22+OR+%22adversarial+attack%22+OR+%22adversarial+suffix%22+OR+%22red-teaming%22+OR+%22red+teaming%22+OR+%22safety+bypass%22+OR+%22guardrail%22+OR+%22many-shot%22+OR+%22cipher+attack%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed URL (XML Atom Feed, Max 50, Newest First)

[Open jailbreak API feed](https://export.arxiv.org/api/query?search_query=(cat:cs.CR+OR+cat:cs.CL+OR+cat:cs.LG)+AND+(abs:"jailbreak"+OR+abs:"jailbreaks"+OR+abs:"jailbreaking"+OR+abs:"adversarial%20suffix"+OR+abs:"red-teaming"+OR+abs:"red%20teaming"+OR+abs:"safety%20bypass")&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=(cat:cs.CR+OR+cat:cs.CL+OR+cat:cs.LG)+AND+(abs:"jailbreak"+OR+abs:"jailbreaks"+OR+abs:"jailbreaking"+OR+abs:"adversarial%20suffix"+OR+abs:"red-teaming"+OR+abs:"red%20teaming"+OR+abs:"safety%20bypass")&sortBy=submittedDate&sortOrder=descending&max_results=50
```

</details>

---

## 4. Experimental Prompts, Prompt Injection & In-Context Dynamics

> **Scope:** Direct / indirect prompt injection, prefill attacks, system prompt extraction, persona modulation, and non-standard prompting.
>
> **Primary categories:** `cs.CL`, `cs.CR`, `cs.AI`

### A — Copy-paste web Boolean query (Abstract / All Fields)

```text
("large language model" OR "LLM") AND ("prompt injection" OR "indirect prompt injection" OR "system prompt" OR "prefill" OR "persona" OR "in-context learning" OR "adversarial prompt" OR "prompt optimization" OR "context manipulation")
```

### B — Prefilled web search URL (All Fields, Newest First)

[Open prompt injection search — all fields, newest first](https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22prompt+injection%22+OR+%22indirect+prompt+injection%22+OR+%22system+prompt%22+OR+%22prefill%22+OR+%22persona%22+OR+%22in-context+learning%22+OR+%22adversarial+prompt%22+OR+%22prompt+optimization%22+OR+%22context+manipulation%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22prompt+injection%22+OR+%22indirect+prompt+injection%22+OR+%22system+prompt%22+OR+%22prefill%22+OR+%22persona%22+OR+%22in-context+learning%22+OR+%22adversarial+prompt%22+OR+%22prompt+optimization%22+OR+%22context+manipulation%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced web search URL (CS Only, Abstract Field, Newest First)

[Open prompt injection search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22prompt+injection%22+OR+%22indirect+prompt+injection%22+OR+%22system+prompt%22+OR+%22prefill%22+OR+%22persona%22+OR+%22in-context+learning%22+OR+%22adversarial+prompt%22+OR+%22prompt+optimization%22+OR+%22context+manipulation%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22prompt+injection%22+OR+%22indirect+prompt+injection%22+OR+%22system+prompt%22+OR+%22prefill%22+OR+%22persona%22+OR+%22in-context+learning%22+OR+%22adversarial+prompt%22+OR+%22prompt+optimization%22+OR+%22context+manipulation%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed URL (XML Atom Feed, Max 50, Newest First)

[Open prompt injection API feed](https://export.arxiv.org/api/query?search_query=(cat:cs.CL+OR+cat:cs.CR+OR+cat:cs.AI)+AND+(abs:"prompt%20injection"+OR+abs:"indirect%20prompt%20injection"+OR+abs:"system%20prompt"+OR+abs:"adversarial%20prompt"+OR+abs:"prompt%20optimization")&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=(cat:cs.CL+OR+cat:cs.CR+OR+cat:cs.AI)+AND+(abs:"prompt%20injection"+OR+abs:"indirect%20prompt%20injection"+OR+abs:"system%20prompt"+OR+abs:"adversarial%20prompt"+OR+abs:"prompt%20optimization")&sortBy=submittedDate&sortOrder=descending&max_results=50
```

</details>

---

## 5. LLM Alignment, RLHF, DPO & Safety Training

> **Scope:** Reinforcement learning from human / AI feedback, direct preference optimization, constitutional AI, unlearning, and refusal mechanisms.
>
> **Primary categories:** `cs.LG`, `cs.CL`, `cs.AI`

### A — Copy-paste web Boolean query (Abstract / All Fields)

```text
("large language model" OR "LLM") AND ("alignment" OR "RLHF" OR "direct preference optimization" OR "DPO" OR "constitutional AI" OR "machine unlearning" OR "refusal" OR "safety alignment" OR "superalignment" OR "reward hacking" OR "deceptive alignment")
```

### B — Prefilled web search URL (All Fields, Newest First)

[Open alignment / RLHF search — all fields, newest first](https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22alignment%22+OR+%22RLHF%22+OR+%22direct+preference+optimization%22+OR+%22DPO%22+OR+%22constitutional+AI%22+OR+%22machine+unlearning%22+OR+%22refusal%22+OR+%22safety+alignment%22+OR+%22superalignment%22+OR+%22reward+hacking%22+OR+%22deceptive+alignment%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22alignment%22+OR+%22RLHF%22+OR+%22direct+preference+optimization%22+OR+%22DPO%22+OR+%22constitutional+AI%22+OR+%22machine+unlearning%22+OR+%22refusal%22+OR+%22safety+alignment%22+OR+%22superalignment%22+OR+%22reward+hacking%22+OR+%22deceptive+alignment%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced web search URL (CS Only, Abstract Field, Newest First)

[Open alignment / RLHF search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22alignment%22+OR+%22RLHF%22+OR+%22direct+preference+optimization%22+OR+%22DPO%22+OR+%22constitutional+AI%22+OR+%22machine+unlearning%22+OR+%22refusal%22+OR+%22safety+alignment%22+OR+%22superalignment%22+OR+%22reward+hacking%22+OR+%22deceptive+alignment%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22alignment%22+OR+%22RLHF%22+OR+%22direct+preference+optimization%22+OR+%22DPO%22+OR+%22constitutional+AI%22+OR+%22machine+unlearning%22+OR+%22refusal%22+OR+%22safety+alignment%22+OR+%22superalignment%22+OR+%22reward+hacking%22+OR+%22deceptive+alignment%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed URL (XML Atom Feed, Max 50, Newest First)

[Open alignment / RLHF API feed](https://export.arxiv.org/api/query?search_query=(cat:cs.LG+OR+cat:cs.CL+OR+cat:cs.AI)+AND+(abs:"safety%20alignment"+OR+abs:"RLHF"+OR+abs:"direct%20preference%20optimization"+OR+abs:"constitutional%20AI"+OR+abs:"machine%20unlearning"+OR+abs:"deceptive%20alignment"+OR+abs:"reward%20hacking")&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=(cat:cs.LG+OR+cat:cs.CL+OR+cat:cs.AI)+AND+(abs:"safety%20alignment"+OR+abs:"RLHF"+OR+abs:"direct%20preference%20optimization"+OR+abs:"constitutional%20AI"+OR+abs:"machine%20unlearning"+OR+abs:"deceptive%20alignment"+OR+abs:"reward%20hacking")&sortBy=submittedDate&sortOrder=descending&max_results=50
```

</details>

---

## 6. Refusal Geometry & Internal Safety Representations (Cross-Over)

> **Scope:** Intersection of latent steering and jailbreaks: refusal directions, orthogonalization, abliteration, and linear representations of harm.
>
> **Primary categories:** `cs.LG`, `cs.CL`, `cs.CR`

### A — Copy-paste web Boolean query (Abstract / All Fields)

```text
("large language model" OR "LLM") AND ("refusal direction" OR "orthogonalization" OR "linear representation" OR "safety representation" OR "representation rerouting" OR "circuit breakers" OR "latent space" OR "hidden states") AND ("jailbreak" OR "safety" OR "alignment" OR "harmful")
```

### B — Prefilled web search URL (All Fields, Newest First)

[Open refusal geometry search — all fields, newest first](https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22refusal+direction%22+OR+%22orthogonalization%22+OR+%22linear+representation%22+OR+%22safety+representation%22+OR+%22representation+rerouting%22+OR+%22circuit+breakers%22+OR+%22latent+space%22+OR+%22hidden+states%22%29+AND+%28%22jailbreak%22+OR+%22safety%22+OR+%22alignment%22+OR+%22harmful%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/?query=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22refusal+direction%22+OR+%22orthogonalization%22+OR+%22linear+representation%22+OR+%22safety+representation%22+OR+%22representation+rerouting%22+OR+%22circuit+breakers%22+OR+%22latent+space%22+OR+%22hidden+states%22%29+AND+%28%22jailbreak%22+OR+%22safety%22+OR+%22alignment%22+OR+%22harmful%22%29&searchtype=all&abstracts=show&order=-announced_date_first&size=50
```

</details>

### C — Prefilled Advanced web search URL (CS Only, Abstract Field, Newest First)

[Open refusal geometry search — CS-only, Abstract field](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22refusal+direction%22+OR+%22orthogonalization%22+OR+%22linear+representation%22+OR+%22safety+representation%22+OR+%22representation+rerouting%22+OR+%22circuit+breakers%22+OR+%22latent+space%22+OR+%22hidden+states%22%29+AND+%28%22jailbreak%22+OR+%22safety%22+OR+%22alignment%22+OR+%22harmful%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)

<details>
<summary>Show raw URL</summary>

```text
https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%28%22large+language+model%22+OR+%22LLM%22%29+AND+%28%22refusal+direction%22+OR+%22orthogonalization%22+OR+%22linear+representation%22+OR+%22safety+representation%22+OR+%22representation+rerouting%22+OR+%22circuit+breakers%22+OR+%22latent+space%22+OR+%22hidden+states%22%29+AND+%28%22jailbreak%22+OR+%22safety%22+OR+%22alignment%22+OR+%22harmful%22%29&terms-0-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first
```

</details>

### D — arXiv API / RSS feed URL (XML Atom Feed, Max 50, Newest First)

[Open refusal geometry API feed](https://export.arxiv.org/api/query?search_query=(cat:cs.LG+OR+cat:cs.CL+OR+cat:cs.CR)+AND+(abs:"refusal%20direction"+OR+abs:"representation%20rerouting"+OR+abs:"circuit%20breakers"+OR+abs:"safety%20representation"+OR+abs:"linear%20representation")&sortBy=submittedDate&sortOrder=descending&max_results=50)

<details>
<summary>Show raw URL</summary>

```text
https://export.arxiv.org/api/query?search_query=(cat:cs.LG+OR+cat:cs.CL+OR+cat:cs.CR)+AND+(abs:"refusal%20direction"+OR+abs:"representation%20rerouting"+OR+abs:"circuit%20breakers"+OR+abs:"safety%20representation"+OR+abs:"linear%20representation")&sortBy=submittedDate&sortOrder=descending&max_results=50
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
