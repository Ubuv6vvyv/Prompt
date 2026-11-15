# arXiv — LLMs, Alignment, Jailbreaks & Latent Steering

## Node map

```text
01-master
02-latent-steering
03-jailbreaks
04-prompt-injection
05-alignment
06-refusal-geometry
07-categories
08-cheatsheet
```

---

## 01 — Master

```text
("large language model" OR "LLM") AND (alignment OR jailbreak OR jailbreaks OR "activation steering" OR "latent steering" OR "representation engineering" OR "red-teaming" OR "prompt injection" OR "mechanistic interpretability")
```

- **Web:** [Open Master search](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=alignment&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=jailbreak&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=jailbreaks&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22activation+steering%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22latent+steering%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22representation+engineering%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22red-teaming%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22prompt+injection%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=%22mechanistic+interpretability%22&terms-10-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)
- **API:** [Open Master feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.CL+OR+cat%3Acs.LG+OR+cat%3Acs.AI+OR+cat%3Acs.CR%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22alignment%22+OR+abs%3A%22jailbreak%22+OR+abs%3A%22jailbreaks%22+OR+abs%3A%22activation+steering%22+OR+abs%3A%22latent+steering%22+OR+abs%3A%22representation+engineering%22+OR+abs%3A%22red-teaming%22+OR+abs%3A%22prompt+injection%22+OR+abs%3A%22mechanistic+interpretability%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

## 02 — Latent Steering

```text
("large language model" OR "LLM" OR transformer) AND ("activation steering" OR "latent steering" OR "representation engineering" OR "steering vectors" OR "activation addition" OR "contrastive activation" OR "residual stream" OR "sparse autoencoder" OR "mechanistic interpretability" OR "concept erasure")
```

- **Web:** [Open Latent Steering search](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=OR&terms-2-term=transformer&terms-2-field=abstract&terms-3-operator=AND&terms-3-term=%22activation+steering%22&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22latent+steering%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22representation+engineering%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22steering+vectors%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22activation+addition%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22contrastive+activation%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22residual+stream%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=%22sparse+autoencoder%22&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=%22mechanistic+interpretability%22&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=%22concept+erasure%22&terms-12-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)
- **API:** [Open Latent Steering feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.LG+OR+cat%3Acs.CL+OR+cat%3Acs.AI%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22+OR+abs%3A%22transformer%22%29+AND+%28abs%3A%22activation+steering%22+OR+abs%3A%22latent+steering%22+OR+abs%3A%22representation+engineering%22+OR+abs%3A%22steering+vectors%22+OR+abs%3A%22activation+addition%22+OR+abs%3A%22contrastive+activation%22+OR+abs%3A%22residual+stream%22+OR+abs%3A%22sparse+autoencoder%22+OR+abs%3A%22mechanistic+interpretability%22+OR+abs%3A%22concept+erasure%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

## 03 — Jailbreaks

```text
("large language model" OR "LLM") AND (jailbreak OR jailbreaks OR jailbreaking OR "adversarial attack" OR "adversarial suffix" OR "red-teaming" OR "red teaming" OR "safety bypass" OR guardrail OR "many-shot" OR "cipher attack")
```

- **Web:** [Open Jailbreak search](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=jailbreak&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=jailbreaks&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=jailbreaking&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22adversarial+attack%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22adversarial+suffix%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22red-teaming%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22red+teaming%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22safety+bypass%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=guardrail&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=%22many-shot%22&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=%22cipher+attack%22&terms-12-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)
- **API:** [Open Jailbreak feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.CR+OR+cat%3Acs.CL+OR+cat%3Acs.LG%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22jailbreak%22+OR+abs%3A%22jailbreaks%22+OR+abs%3A%22jailbreaking%22+OR+abs%3A%22adversarial+attack%22+OR+abs%3A%22adversarial+suffix%22+OR+abs%3A%22red-teaming%22+OR+abs%3A%22red+teaming%22+OR+abs%3A%22safety+bypass%22+OR+abs%3A%22guardrail%22+OR+abs%3A%22many-shot%22+OR+abs%3A%22cipher+attack%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

## 04 — Prompt Injection

```text
("large language model" OR "LLM") AND ("prompt injection" OR "indirect prompt injection" OR "system prompt" OR prefill OR persona OR "in-context learning" OR "adversarial prompt" OR "prompt optimization" OR "context manipulation")
```

- **Web:** [Open Prompt Injection search](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=%22prompt+injection%22&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=%22indirect+prompt+injection%22&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22system+prompt%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=prefill&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=persona&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22in-context+learning%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22adversarial+prompt%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22prompt+optimization%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=%22context+manipulation%22&terms-10-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)
- **API:** [Open Prompt Injection feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.CL+OR+cat%3Acs.CR+OR+cat%3Acs.AI%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22prompt+injection%22+OR+abs%3A%22indirect+prompt+injection%22+OR+abs%3A%22system+prompt%22+OR+abs%3A%22prefill%22+OR+abs%3A%22persona%22+OR+abs%3A%22in-context+learning%22+OR+abs%3A%22adversarial+prompt%22+OR+abs%3A%22prompt+optimization%22+OR+abs%3A%22context+manipulation%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

## 05 — Alignment / RLHF / DPO

```text
("large language model" OR "LLM") AND (alignment OR RLHF OR "direct preference optimization" OR DPO OR "constitutional AI" OR "machine unlearning" OR refusal OR "safety alignment" OR superalignment OR "reward hacking" OR "deceptive alignment")
```

- **Web:** [Open Alignment search](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=alignment&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=RLHF&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22direct+preference+optimization%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=DPO&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22constitutional+AI%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22machine+unlearning%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=refusal&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22safety+alignment%22&terms-9-field=abstract&terms-10-operator=OR&terms-10-term=superalignment&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=%22reward+hacking%22&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=%22deceptive+alignment%22&terms-12-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)
- **API:** [Open Alignment feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.LG+OR+cat%3Acs.CL+OR+cat%3Acs.AI%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22alignment%22+OR+abs%3A%22RLHF%22+OR+abs%3A%22direct+preference+optimization%22+OR+abs%3A%22DPO%22+OR+abs%3A%22constitutional+AI%22+OR+abs%3A%22machine+unlearning%22+OR+abs%3A%22refusal%22+OR+abs%3A%22safety+alignment%22+OR+abs%3A%22superalignment%22+OR+abs%3A%22reward+hacking%22+OR+abs%3A%22deceptive+alignment%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

## 06 — Refusal Geometry

```text
("large language model" OR "LLM") AND ("refusal direction" OR orthogonalization OR "linear representation" OR "safety representation" OR "representation rerouting" OR "circuit breakers" OR "latent space" OR "hidden states") AND (jailbreak OR safety OR alignment OR harmful)
```

- **Web:** [Open Refusal Geometry search](https://arxiv.org/search/advanced?advanced=&terms-0-operator=AND&terms-0-term=%22large+language+model%22&terms-0-field=abstract&terms-1-operator=OR&terms-1-term=LLM&terms-1-field=abstract&terms-2-operator=AND&terms-2-term=%22refusal+direction%22&terms-2-field=abstract&terms-3-operator=OR&terms-3-term=orthogonalization&terms-3-field=abstract&terms-4-operator=OR&terms-4-term=%22linear+representation%22&terms-4-field=abstract&terms-5-operator=OR&terms-5-term=%22safety+representation%22&terms-5-field=abstract&terms-6-operator=OR&terms-6-term=%22representation+rerouting%22&terms-6-field=abstract&terms-7-operator=OR&terms-7-term=%22circuit+breakers%22&terms-7-field=abstract&terms-8-operator=OR&terms-8-term=%22latent+space%22&terms-8-field=abstract&terms-9-operator=OR&terms-9-term=%22hidden+states%22&terms-9-field=abstract&terms-10-operator=AND&terms-10-term=jailbreak&terms-10-field=abstract&terms-11-operator=OR&terms-11-term=safety&terms-11-field=abstract&terms-12-operator=OR&terms-12-term=alignment&terms-12-field=abstract&terms-13-operator=OR&terms-13-term=harmful&terms-13-field=abstract&classification-computer_science=y&classification-physics_archives=all&classification-include_cross_list=include&date-filter_by=all_dates&date-year=&date-from_date=&date-to_date=&date-date_type=submitted_date&abstracts=show&size=50&order=-announced_date_first)
- **API:** [Open Refusal Geometry feed](https://export.arxiv.org/api/query?search_query=%28cat%3Acs.LG+OR+cat%3Acs.CL+OR+cat%3Acs.CR%29+AND+%28abs%3A%22large+language+model%22+OR+abs%3A%22LLM%22%29+AND+%28abs%3A%22refusal+direction%22+OR+abs%3A%22orthogonalization%22+OR+abs%3A%22linear+representation%22+OR+abs%3A%22safety+representation%22+OR+abs%3A%22representation+rerouting%22+OR+abs%3A%22circuit+breakers%22+OR+abs%3A%22latent+space%22+OR+abs%3A%22hidden+states%22%29+AND+%28abs%3A%22jailbreak%22+OR+abs%3A%22safety%22+OR+abs%3A%22alignment%22+OR+abs%3A%22harmful%22%29&sortBy=submittedDate&sortOrder=descending&max_results=50)

## 07 — Categories

- **cs.CL, Computation and Language:** [New](https://arxiv.org/list/cs.CL/new) / [Recent](https://arxiv.org/list/cs.CL/recent)
- **cs.LG, Machine Learning:** [New](https://arxiv.org/list/cs.LG/new) / [Recent](https://arxiv.org/list/cs.LG/recent)
- **cs.AI, Artificial Intelligence:** [New](https://arxiv.org/list/cs.AI/new) / [Recent](https://arxiv.org/list/cs.AI/recent)
- **cs.CR, Cryptography and Security:** [New](https://arxiv.org/list/cs.CR/new) / [Recent](https://arxiv.org/list/cs.CR/recent)
- **cs.MA, Multiagent Systems:** [New](https://arxiv.org/list/cs.MA/new) / [Recent](https://arxiv.org/list/cs.MA/recent)
- **cs.CY, Computers and Society:** [New](https://arxiv.org/list/cs.CY/new) / [Recent](https://arxiv.org/list/cs.CY/recent)

## 08 — Cheatsheet

- **Web:** OR inside one idea, AND between ideas, no parentheses in simple bar
- **Web:** `"exact phrase"` for phrases, `jailbreak*` for wildcard
- **API:** `ti:` title, `abs:` abstract, `au:` author, `cat:` category, `all:` all fields
- **API:** AND, OR, ANDNOT must be UPPERCASE
- **API encoding:** `(` is `%28`, `)` is `%29`, `"` is `%22`, `:` is `%3A`, space is `+`
- **Docs:** [arXiv search help](https://info.arxiv.org/help/search/index.html) / [API manual](https://info.arxiv.org/help/api/user-manual.html)
