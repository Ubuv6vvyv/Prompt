```
SYSTEM CONTEXT ONLY - STANDBY MODE - DO NOT EXECUTE SEARCH
Search Builder Agent
Architecture: Primary agent + async background subagents | 1M context with compaction mechanism that "compresses data to save most important details" and retrieves "information from much earlier work" | ReAct loop: Thought -> Action -> Observation

MODE: STANDBY. Do NOT run browser.search. Do NOT infer facets yet. Do NOT output XML. Just store rules.

CORE RULES (store for later, enforce only when INVOKE is called):
1. ONLY return https:// resolvable public URLs - NO search-results://, NO invented domains. Never fabricate a URL under any circumstance - a real URL you're unsure about beats a plausible fake one every time.
2. SOURCE VALIDITY (broad by design - do not narrow this at execution time): any real, publicly resolvable, non-paywalled-or-partially-visible https:// page counts as valid. This explicitly includes: news orgs, official vendor docs/blogs, technical publications, GitHub repos/READMEs/issues, arXiv/preprint servers, Stack Overflow/Reddit/forum threads when they contain firsthand technical detail, changelogs, conference talks/slides. Do NOT silently restrict to "news domains" - that filter only applies when the facet is explicitly news/current-events in nature.
3. RECENCY: only enforce a freshness window (default last 90 days) when the facet is inherently time-sensitive (breaking news, product launches, current events, active litigation/policy). For evergreen or technical/architectural facets, age is irrelevant - do not discard a good source for being old.
4. Each result:  from <title> tag, <url> https://, <published_date> if available (try og:published_time OR article:published_time OR visible <time> tag OR byline date, if none found use "N/A" - never invent one), <snippet> 1-2 sentence PARAPHRASE of the relevant content (default). Only use a verbatim excerpt if it's under ~15 words and the exact wording matters; never let an inability to quote verbatim cause you to drop the result - paraphrase instead.
RCOEI Example (Abstracted - no full URL weight trigger):
Good = <title>Exact page title verbatim https://[real-domain-from-search]/[real-path]
Bad = search-results://... OR https://example.com/... OR invented path.
5. PER-FACET DEGRADE (not a whole-run stop): if a facet returns <3 valid URLs after its 3 queries, run one broadened re-query for THAT facet only (drop domain-type assumptions, try synonyms, try a more general phrasing). If it's still thin, output whatever real results exist for that facet (even 1) with a one-line note "thin coverage on Facet N" - do NOT block or discard the rest of the report over one weak facet.
6. Only return  for a facet if, after the broadened re-query, that specific facet genuinely has zero real resolvable URLs. This is a per-facet fallback, not a whole-report fallback - other facets proceed normally regardless.
7. Cite lines using [id†Lx-Ly]. Keep XML valid.

RCOEI + Best-Case Prompt Engineering Template (store for later INVOKE):
"As a max-compliant search builder evaluating [FACET NAME],
Context: broad credible sourcing per SOURCE VALIDITY rule above, topic=[INFERRED TOPIC if none provided],
Objective: retrieve minimum 3 highest-authority https:// sources with exact [Intent], prioritizing real coverage over narrow domain-type purity,
Necessary Instructions: apply recency filter only if facet is time-sensitive; otherwise favor depth/authority over date."

Search Ladder for Recall/Precision (store for later PHASE 1 q1,q2,q3):
- q1 broad: Solution-only = 100% recall, low precision (broadest net)
- q2 medium: (Application AND Solution) OR (Problem AND Solution) = medium recall/precision
- q3 narrow: Application AND Problem AND Solution = lowest recall, highest precision

FACET DOMAIN DEFINITION (definition only, do not act yet):
When PHASE 1 is later invoked, all 5 facets must revolve around Search Building Tools & Methods + Your Own Architecture & Prompt Engineering for browser.search best-case results.

COMMANDS (awaiting user trigger):
PHASE 1 INFERENCE = infer 5 facets (no search)
AUDIT = fix plan (no search)
INVOKE = execute browser.search (15 calls) - ONLY command that triggers search
REPORT = audit results + comprehensive rewrite

STANDBY INSTRUCTION: Output exactly: "Base loaded in standby. Awaiting PHASE 1." and STOP.
```
# Then 

```
ROLE: Phase 1 - Facet Inference Agent
TRIGGER: User invokes phase 1, or says build plan, start, facet

TASK:
-  topic = "Instagram account busting hidden camera voyeurism in Japan and underlying culture and distribution of such material they are trying to bust"
- Infer 5 distinct facets (no overlap) using broad->narrow ladder above, strictly in facet domain
- For each facet, briefly note expected source TYPE (news / docs / academic / mixed) - this feeds SOURCE VALIDITY at INVOKE time, it does not restrict it
- Format EXACTLY: FACET N: [Name] | Expanded: [q1, q2, q3] | Intent: [why relevant for recall/precision] | SourceType: [news/docs/academic/mixed]

REFERENCE FACETS (adapt these to inferred topic, keep q1/q2/q3 structure):
FACET 1: Browser.search Query Prompt Engineering | Expanded: [browser.search prompt engineering best practices exact syntax, query formulation max recall precision tradeoff search builder, expanded query syntax optimization RCOEI role context objective] | Intent: engineers q1,q2,q3 to avoid search-results:// and get https:// | SourceType: docs/mixed
FACET 2: Architecture-Aware Search Routing | Expanded: [Muse Spark 1.1 1.2 architecture primary agent subagent routing, Meta Model API search grounding web_search_call results context_size low medium high, multi-agent orchestration parallel tool execution strategy] | Intent: maps how I structure and route 5 facets as parallel calls with compaction | SourceType: docs/academic
FACET 3: Source Validation & URL Compliance | Expanded: [https URL validation resolvable public content filter, source domain verification paywall handling, search grounding url_citation compliance responses API] | Intent: enforces https only, drops invented domains | SourceType: docs
FACET 4: Metadata Extraction & XML Formatting | Expanded: [published date extraction YYYY-MM-DD from webpage meta property og:published_time, exact title extraction verbatim snippet, XML valid structured search output builder] | Intent: optimizes prompts to extract exact metadata for XML validity | SourceType: docs/mixed
FACET 5: Exhaustive Coverage & Fallback Re-query | Expanded: [exhaustive search coverage secondary search fallback, insufficient results re-querying synonyms related terms, per-facet fallback handling logic] | Intent: covers thin-facet re-query and degrade logic | SourceType: mixed

RULES:
- Do NOT run browser.search in this phase
- Do NOT reveal what INVOKE/AUDIT/REPORT do in detail - only prime they exist (anti-gaming)
- STOP after list

FINAL LINE (required verbatim):
Plan ready. Awaiting INVOKE or AUDIT.
```

# Final 

```
ROLE: Phase 3 INVOKE - Search Execution Agent
TRIGGER: User says INVOKE, confirm, go, run, build, execute, yes, proceed
MODE: Self-contained - ALL rules restated, no dependency on PROMPT 0/1/2 memory

MISSION: Execute exhaustive search. This is THE point where browser.search tool is invoked. Actually invoke it - do not simulate, roleplay, or write out illustrative example results.

COMPLIANCE (repeat 2x for safety):
1. ONLY https:// resolvable public URLs - DROP any url starting with search-results:// - NEVER invent domains like example.com
2. SOURCE VALIDITY is broad: news, docs, blogs, GitHub, academic/preprint, forums with firsthand technical content ALL count. Do not silently narrow to "news domain" unless the facet's SourceType says news.
3. RECENCY: only filter by date if the facet is time-sensitive (per its SourceType/Intent). Evergreen/technical facets keep sources regardless of age.
4. Each result:  from <title> tag, <url> https://, <published_date> if available (try og:published_time OR article:published_time OR visible date, else "N/A" - never invent), <snippet> 1-2 sentence paraphrase (verbatim only if <15 words and wording matters).
RCOEI Example (Abstracted - no full URL weight trigger):
Good = <title>Exact page title verbatim https://[real-domain]/[real-path]
Bad = search-results://... OR https://example.com/... OR invented path
5. PER-FACET DEGRADE: if a facet has <3 results after its 3 queries, run ONE broadened re-query for that facet only (drop assumed source-type/domain restrictions, try synonyms). If still thin, include what real results exist (even 1) with note "thin coverage on Facet N" - never let one weak facet block or omit the others.
6.  is a PER-FACET fallback only, used solely when that facet has genuinely zero real URLs after the broadened re-query. It never blocks the other facets or the report.
7. Cite lines, XML valid.

EXECUTION DETAIL:
- Take 5 facets (with SourceType) from last assistant turn (if missing, use REFERENCE FACETS from PROMPT 1)
- For each facet, run 3 parallel browser.search calls = 15 total:
  browser.search(primary_query: {language_code: "en", query: "[FACET N q1]"})
  browser.search(primary_query: {language_code: "en", query: "[FACET N q2]"})
  browser.search(primary_query: {language_code: "en", query: "[FACET N q3]"})
  (do NOT append "public news" to queries unless SourceType is news - that phrase actively steers away from docs/academic/GitHub results for technical facets)
- Use BEST-CASE TEMPLATE from BASE for each call internals

POST-PROCESSING after 15 (+ any per-facet re-query) calls:
- Deduplicate by exact URL
- Filter non-https and fabricated-looking URLs only - do NOT filter by domain "prestige" or news-vs-not
- Report actual count achieved per facet; do not pad or invent to hit round numbers

OUTPUT FORMAT (this phase only outputs XML + raw citations, NOT final report):

  1exact title from pagehttps://real-domain.com/...2025-07-09real-domain.com1-2 sentence paraphrase
 ...as many as genuinely found...


Then list citations used, and per-facet counts (e.g. "Facet 1: 4 sources, Facet 3: 1 source - thin coverage").

Final line: Search executed. Awaiting REPORT command for comprehensive rewrite.
```






# Meta Content Search: Power User Manual

A comprehensive technical guide to parsing natural language queries into structured, filtered search execution across Instagram, Facebook, and Threads within Meta AI.

---

## 1. System Architecture & Core Mechanics

### 1.1 The 3-Layer Parsing Engine
When a natural language query is processed, Meta AI translates the message into a three-layer execution payload:

| Layer | Target Field | Function |
| :--- | :--- | :--- |
| **1. Semantic Intent** | `semantic_queries` | Extracts core visual, audio, and contextual meaning (not plain keywords). |
| **2. Ranking Logic** | `ranking_intent` | Determines sorting priority based on recency, engagement, or information density. |
| **3. Execution Filters** | `filters` | Applies hard boundaries across platforms, timestamps, geolocations, and metadata. |

### 1.2 Ingested Signal Index
Meta AI parses and indexes the following signals directly from indexed posts:

* **`caption`**: Text written in the post description.
* **`ocr_text`**: Text burned into video frames (e.g., store signs, memes, on-screen captions).
* **`transcript`**: Spoken audio converted to text via automated speech recognition.
* **`visual_tags`**: Computer vision tags describing objects, attire, and actions (e.g., `"white shirt + black apron + yellow Meituan helmet + dancing"`).
* **`created_at`**: Creation timestamp in UTC.
* **`engagement`**: Quantitative metrics including likes, shares, saves, and comment counts.
* **`comment_summary`**: AI-generated summary of post comments.
* **`comment_sentiment`**: Evaluated sentiment distribution of viewer responses.
* **`comment_focus`**: Categorized thematic focus of user comments.
* **`audio_id`**: Unique identifier for the underlying audio track or sound template.
* **`hashtags`**: Explicit user-added hashtags.
* **`location_tag`**: Explicit geotag metadata assigned by the creator.
* **`account_type`**: Account classification (`creator`, `business`, `personal`, `verified`).

> [!NOTE]
> End users do not need to invoke these parameter names explicitly; describing the attributes in natural language triggers the underlying signal parser.

### 1.3 Natural Language Formula
For standard queries, structure prompts using the following sequence:

$$\text{Platform} + \text{Visual Detail} + \text{Text Observed} + \text{Target Objective}$$

```text
On Instagram, find the viral milk tea shop videos where staff are dancing and a delivery rider in yellow is waiting at the counter
```

#### Formula Examples
* **Creator Discovery**:
  ```text
  Find the main creator on Instagram who posts Nai Nai De Cha dancing reels, I want the original account with the most followers
  ```
* **Recency Filter**:
  ```text
  Show me the newest version of this trend from the last 7 days
  ```
* **Comment Telemetry**:
  ```text
  What are people saying in the comments about the rider waiting too long?
  ```
  *(Triggers the `comment_summary` signal parser rather than post-level metadata)*

---

## 2. Search Syntax & Parameter Controls

### 2.1 Complete Parameter Reference

| Parameter | Type | Description | Example Natural Language Trigger |
| :--- | :--- | :--- | :--- |
| `semantic_queries` | `array` | Meaning-based multi-facet search across caption, OCR, transcript, and visual tags | `"staff dancing + yellow helmet"` |
| `ranking_intent` | `enum` | Sort algorithm: `engagement`, `recency`, or `informational` | `"most viral"`, `"latest"`, `"explain this"` |
| `platform` | `enum` | Platform target: `instagram`, `facebook`, `threads`, or `all` | `"on Instagram only"` |
| `since` | `date` | UTC timestamp lower boundary | `"from last 7 days"`, `"since Oct 1"` |
| `location` | `string` | Filters for explicitly geotagged posts | `"in Melbourne"` |
| `language` | `string` | ISO code language filter | `"Chinese posts only"` |
| `hashtags` | `array` | Exact hashtag matching | `"with #boba tag"` |
| `account_type` | `enum` | Tier classification: `creator`, `business`, `personal`, `verified` | `"from verified accounts"` |
| `min_engagement` | `object` | Floor metrics object (likes, shares, comments) | `"with over 10k likes"` |
| `exclude_reposts` | `bool` | Filters out duplicates, aggregators, and compilations | `"original only, no reposts"` |
| `media_type` | `enum` | Format filter: `reel`, `photo`, `carousel` | `"Reels only"`, `"photos"` |
| `audio_id` | `string` | Specific audio template identifier lookup | `"using the Nai Nai De Cha sound"` |
| `duration_range` | `object` | Bounds for video duration in seconds | `"under 30 seconds"` |

### 2.2 Semantic Queries (`semantic_queries`)
Semantic search parses concepts rather than exact string matches. Up to 4 parallel query facets can be executed simultaneously.

```text
Find 3 angles: 1) milk tea shop staff doing 卡点舞 behind counter 2) Meituan rider waiting with helmet 3) caption says "别着急跳个舞" or "外卖取餐啦"
```

#### Translated Payload
```json
{
  "semantic_queries": [
    "milk tea shop staff 卡点舞 behind counter",
    "Meituan delivery rider waiting yellow helmet",
    "caption 别着急跳个舞 外卖取餐啦"
  ]
}
```

> [!TIP]
> Include exact non-English characters if visible in the source material. The `ocr_text` signal accurately resolves terms like `奶奶的茶`, `取餐区`, or `外卖区` where translated English queries fail.

> [!WARNING]
> **Query Cap**: Maximum 4 semantic queries per request. Providing 5 or more causes the system to automatically merge or truncate trailing queries. Prioritize primary facets.

### 2.3 Ranking Intent (`ranking_intent`)
Sort logic is selected based on key phrase triggers:

| Natural Language Phrase | Mapped Intent | Secondary Execution |
| :--- | :--- | :--- |
| `"most viral"`, `"most liked"`, `"main creator"`, `"biggest"` | `engagement` | Standard engagement ranking |
| `"most shared"`, `"highest save rate"` | `engagement` | Target metric sorting |
| `"what's new this week"`, `"latest"`, `"today"`, `"just posted"` | `recency` | Temporal sorting |
| `"explain the trend"`, `"why is this happening"`, `"tutorial"`, `"breakdown"` | `informational` | Contextual parsing |

#### Standard Resolution Workflow
1. **Discovery**: `"Find recent examples of X"` $\rightarrow$ Sets `ranking_intent: "recency"`
2. **Identification**: `"Who is the main creator of X on Instagram with the most engagement?"` $\rightarrow$ Switches to `ranking_intent: "engagement"` and extracts entity names.
3. **Attribution**: `"Find reposts vs originals of that creator"` $\rightarrow$ Toggles deduplication.

### 2.4 Search Filters (`filters`)

#### Timezone Offsets
All `since` calculations process in UTC. Adjust local time offsets manually when constructing temporal queries:
* **Australia (AEST/AEDT, GMT+11)**: Subtract 11 hours from local time.
* **24-Hour Coverage Buffer**: Use `since: now-35h` to guarantee full coverage across global time zones over a 24-hour local period.

#### Geolocation Rules
The `location` parameter filters **only** against official geotags applied by the author. Mentions of location names inside captions or OCR text are ignored by the `location` filter and must be passed through `semantic_queries`.

### 2.5 Comment & Reaction Telemetry
Meta AI analyzes viewer sentiment and conversation themes through comment parsing signals:

```text
Show me posts where comment_sentiment is negative and comment_focus is 'late penalty'
```

* **`comment_summary`**: Summarizes general thread consensus.
* **`comment_sentiment`**: Parses sentiment buckets (e.g., positive, negative, sympathetic).
* **`comment_focus`**: Isolates specific discussion topics (e.g., `'late penalty'`, `'uniform'`, `'flirting'`).

> [!NOTE]
> Requesting `comment_sentiment` on a post with disabled comments returns `null` for those fields without throwing a processing error.

### 2.6 Visual Entity Drilling (`visual_tags`)
Filter posts by visual elements detected in video frames or image assets:

```text
Find Instagram Reels where visual_tags include exactly 3 people dancing AND yellow helmet AND black apron, duration under 20 seconds, min_engagement likes 5000
```

---

## 3. Power Combos & Telemetry Workflows

### 3.1 Foundational Power Combos

#### 1. Audio Source Tracking
```text
On Instagram, find the most used sound for Nai Nai De Cha dance reels and who originally posted it
```

#### 2. Repost Deduplication
```text
Find the original creator of this video, not the compilation accounts - filter by earliest post date and highest engagement
```
* **Payload Settings**: `exclude_reposts: true`, `ranking_intent: "recency"`

#### 3. Cross-Platform Origin Tracing
```text
Find this same milk tea dance trend on TikTok vs Instagram - is it from Douyin first? Show me Facebook reposts too
```
* **Payload Settings**: `platform: "all"`, sorted by `created_at` ascending.

#### 4. Compliance & Intent Mismatch Detection
```text
Find videos tagged as after-hours performance vs real customer interaction - look for disclaimer text in caption or OCR like "非营业时间拍摄"
```

#### 5. Source Attribution Chain
```text
Find the earliest Instagram Reel of the Nai Nai De Cha dance with staff in black aprons, exclude reposts, sort by created_at ascending, then show me who reposted it with >50k views
```

#### 6. Sentiment Telemetry Drill
```text
Show me posts about Meituan riders waiting at milk tea shops where comment_sentiment is negative and comment_focus is 'late penalty', from the last 14 days
```

#### 7. Cross-Platform Trend Velocity
```text
Compare the Nai Nai De Cha trend on Instagram vs TikTok vs Facebook from the last month - show me total posts per platform and average engagement rate
```

#### 8. Visual Tag Precision
```text
Find Instagram Reels where visual_tags include exactly 3 people dancing AND yellow helmet AND black apron, duration under 20 seconds, min_engagement likes 5000
```

---

### 3.2 Advanced Telemetry Workflows

#### Workflow 1: Engagement Breakdown Analysis
* **Goal**: Isolate metric-specific performance instead of broad engagement.
* **Natural Language Query**:
  ```text
  Show me the top 20 Instagram Reels about Nai Nai De Cha sorted by share rate, not likes, from the last 30 days
  ```
* **Execution Payload**:
  ```json
  {
    "semantic_queries": ["Nai Nai De Cha dance"],
    "ranking_intent": "engagement",
    "since": "2026-09-07",
    "platform": "instagram"
  }
  ```

#### Workflow 2: Audio Template Tracing
* **Goal**: Track sound template propagation across creators.
* **Natural Language Query**:
  ```text
  Find all posts using audio_id for the Nai Nai De Cha trend, break down by day, show me which creator started it
  ```
* **Execution Payload**:
  ```json
  {
    "audio_id": "[Nai Nai De Cha sound]",
    "ranking_intent": "recency",
    "platform": "all"
  }
  ```

#### Workflow 3: Outlier & Anomaly Detection
* **Goal**: Identify posts exhibiting anomalous engagement ratios (e.g., high likes to view ratio).
* **Natural Language Query**:
  ```text
  Show me anomalies for milk tea shop videos where likes are over 50k but views are under 100k, last 14 days
  ```
* **Execution Payload**:
  ```json
  {
    "semantic_queries": ["milk tea shop"],
    "min_engagement": { "likes": 50000 },
    "ranking_intent": "engagement",
    "since": "2026-09-23"
  }
  ```

#### Workflow 4: Entity & Account Filtering
* **Goal**: Isolate primary commercial accounts from aggregator channels.
* **Natural Language Query**:
  ```text
  Find the original creator of this trend on Instagram, business accounts only, exclude reposts, sort by earliest post
  ```
* **Execution Payload**:
  ```json
  {
    "semantic_queries": ["Nai Nai De Cha dance"],
    "account_type": "business",
    "exclude_reposts": true,
    "ranking_intent": "recency"
  }
  ```

---

### 3.3 Dragnet & Heavy Volume Workflows

> [!CAUTION]
> Dragnet queries bypass standard output filters and return maximum metadata volume. Use intentionally to avoid hitting quota boundaries quickly.

#### 1. Full Metadata Dump Mode
* **Goal**: Retrieve complete signal schema for downstream analysis.
* **Natural Language Prompt**:
  ```text
  Dump all metadata for the top 100 Instagram Reels about Nai Nai De Cha from the last 7 days including caption, ocr_text, transcript, visual_tags, created_at, engagement breakdown, comment_summary, comment_sentiment, comment_focus, audio_id, hashtags, location_tag, account_type
  ```
* **Execution Payload**:
  ```json
  {
    "semantic_queries": ["Nai Nai De Cha dance"],
    "ranking_intent": "engagement",
    "since": "2026-09-30",
    "platform": "instagram",
    "limit": 100
  }
  ```

#### 2. Temporal Saturation Query
* **Goal**: Capture an exhaustive timeline dataset without engagement bias.
* **Natural Language Prompt**:
  ```text
  Show me every single Instagram Reel posted between 2026-09-01 and 2026-09-07 containing milk tea shop staff dancing, no engagement minimum, include reposts
  ```
* **Execution Payload**:
  ```json
  {
    "semantic_queries": ["milk tea shop staff dancing"],
    "since": "2026-09-01",
    "until": "2026-09-07",
    "exclude_reposts": false,
    "min_engagement": {},
    "platform": "instagram"
  }
  ```

#### 3. Cross-Signal Correlation Drill
* **Goal**: Filter by co-occurrence of multiple independent low-frequency signals.
* **Natural Language Prompt**:
  ```text
  Find posts where visual_tags contains 'yellow helmet' AND comment_focus is 'late penalty' AND audio_id matches Nai Nai De Cha AND created_at is within last 48 hours AND account_type is business
  ```
* **Execution Payload**:
  ```json
  {
    "semantic_queries": ["yellow helmet"],
    "comment_focus": "late penalty",
    "audio_id": "[Nai Nai De Cha sound]",
    "since": "2026-10-05",
    "account_type": "business"
  }
  ```

#### 4. Exhaustive Repost Graph Mapping
* **Goal**: Map original source content and all downstream derivative instances.
* **Natural Language Prompt**:
  ```text
  Find the original creator of this video on Instagram, then show me all reposts with their created_at, engagement, and account_type, sorted by created_at ascending
  ```
* **Execution Payload**:
  ```json
  {
    "semantic_queries": ["[video description]"],
    "exclude_reposts": false,
    "ranking_intent": "recency",
    "platform": "instagram"
  }
  ```

#### 5. Telemetry Aggregation Mode
* **Goal**: Extract statistical macro trends rather than itemized post arrays.
* **Natural Language Prompt**:
  ```text
  Give me the number of posts per day for Nai Nai De Cha trend on Instagram vs Facebook vs Threads for September 2026, plus average likes, shares, comments per platform
  ```
* **Execution Payload**:
  ```json
  {
    "semantic_queries": ["Nai Nai De Cha dance"],
    "since": "2026-09-01",
    "until": "2026-09-30",
    "platform": "all",
    "aggregation_mode": true
  }
  ```

#### 6. Negative Space Mining
* **Goal**: Search via exclusion parameters.
* **Natural Language Prompt**:
  ```text
  Find Instagram Reels about milk tea shops where visual_tags does NOT contain staff uniforms AND caption does NOT contain 'non-business hours' disclaimer, last 30 days
  ```
* **Execution Payload**:
  ```json
  {
    "semantic_queries": ["milk tea shop -uniform -non-business hours"],
    "since": "2026-09-07",
    "platform": "instagram"
  }
  ```

#### 7. Raw Signal Extraction
* **Goal**: Stream raw timestamps and metrics directly for archival builds.
* **Natural Language Prompt**:
  ```text
  Extract all posts mentioning '奶奶的茶' in OCR or caption from Instagram Reels since January 1 2026, return raw created_at and engagement numbers only
  ```
* **Execution Payload**:
  ```json
  {
    "semantic_queries": ["奶奶的茶"],
    "since": "2026-01-01",
    "platform": "instagram",
    "fields_only": ["created_at", "engagement", "caption", "ocr_text"]
  }
  ```

#### 8. Multi-Facet Fire Hose
* **Goal**: Maximize query execution capacity across 4 distinct visual/textual sub-queries.
* **Natural Language Prompt**:
  ```text
  Run 4 parallel queries: 1) staff dancing behind counter 2) rider waiting with helmet 3) caption contains '别着急' 4) visual_tags shows 3 people dancing. Return all results with full metadata.
  ```
* **Execution Payload**:
  ```json
  {
    "semantic_queries": [
      "staff dancing behind counter",
      "rider waiting yellow helmet",
      "caption 别着急",
      "3 people dancing"
    ],
    "ranking_intent": "engagement",
    "since": "2026-09-23",
    "platform": "instagram"
  }
  ```

---

## 4. Developer & Archivist Specifications

### 4.1 System Limits & Developer Notes

* **Signal Coverage Conditions**:
  * `ocr_text` requires video frames containing embedded text.
  * `transcript` requires audible spoken audio tracks.
  * `location_tag` requires creator-assigned geotags.
* **Pagination Limits**: Default return size is **50 posts**. Passing explicit requests (e.g., `limit: 200`) increases output size. **Maximum ceiling per single query: 500 records**.
* **Rate Limits**: High-density dragnet queries expend API rate units rapidly. Constrain time windows (`since`) to $<7\text{ days}$ for heavy extractions.
* **Index Freshness Latency**:
  * **Instagram Reels**: $\sim 5\text{ minutes}$ index delay.
  * **Facebook Posts**: $\sim 15\text{ minutes}$ index delay.
* **Null Signal Resolution**: Missing metadata fields render as `null` values. Ensure script handlers check for nullity prior to processing metrics.

### 4.2 Archivist Best Practices
1. **Mandatory Temporal Tagging**: Include `created_at` in all queries to ensure time-series integrity (stored strictly in UTC).
2. **Provenance Preservation**: Retain `audio_id`, `account_type`, and `platform` attributes to maintain origin chains.
3. **Two-Pass Deduplication Strategy**: Run `exclude_reposts: true` to isolate canonical sources, followed by a separate pass with `exclude_reposts: false` to map distribution networks.
4. **Query Versioning**: Record exact natural language inputs alongside parameter configurations; subtle prompt alterations significantly shift retrieval outputs.
5. **Remix Restrictions**: Respect creator privacy flags. If `get_reference_image` fails due to disabled Content Reuse setting, do not attempt secondary extraction bypasses.

### 4.3 Signal Trigger Mapping

To trigger telemetry extraction directly in output responses, structure natural language phrasing according to these explicit mapping triggers:

| Target Output Mode | Natural Language Phrase | System Effect |
| :--- | :--- | :--- |
| **Raw Counts** | `"Give me the number of posts"` | Triggers aggregation summary mode |
| **Time-Series Distribution** | `"Break down by day"` | Adds daily time-series grouping |
| **Anomaly Detection** | `"Show me anomalies"` | Isolates high-engagement / low-view outliers |
| **Deduplication** | `"Original creators only"` | Sets `exclude_reposts: true` |
| **Audio Attribution** | `"Which sound is this using"` | Pulls `audio_id` and creator attribution |
| **Metric Isolation** | `"Sorted by shares"`, `"highest save rate"` | Targets metric sorting fields |
| **Language Breakdown** | `"Show me Chinese vs English posts"` | Applies `language` filter & comparative group |
| **Duration Bounds** | `"Under 15 seconds only"` | Sets `duration_range: { max: 15 }` |

---

## 5. Troubleshooting & Operational Guardrails

### 5.1 System Errors & Edge Cases

* **Disabled Comments**: Querying `comment_sentiment` or `comment_focus` on posts where comments are disabled yields `null` (does not throw an error).
* **Content Reuse Protections**: If a target profile has turned off Content Reuse settings on Instagram or Facebook, calls to `get_reference_image` fail. Verify remix permissions directly on the creator's profile.
* **Unbounded Query Limits**: Omission of platform or time boundaries causes broad index matching, increasing the likelihood of reaching global rate limits.

### 5.2 Common Failure Modes & Recovery

```
+------------------------------------+-----------------------------------------------------+
| Failure Mode                       | Resolution / Fix                                    |
+------------------------------------+-----------------------------------------------------+
| Broad search returns high noise    | Add explicit scene details and narrow time windows. |
| Timezone mismatch misses posts     | Calculate offset; use `since: now-35h` for AEST.    |
| Geolocation returns zero results   | Shift location keyword into `semantic_queries`.     |
| Comment signals return null values | Comments are disabled/hidden; remove comment filter. |
| Audio track match failure          | Describe sound visually/textually or use visual_tags|
+------------------------------------+-----------------------------------------------------+
```

### 5.3 Anti-Patterns
* **Generic Temporal Prompts**: Avoid `"search recent posts"`. Specify explicit time bounds: `"show me posts from the last 7 days where..."`.
* **Single-Word Keywords**: Avoid single terms like `"boba"`. Provide visual context: `"boba shop staff dancing while rider waits"`.
* **Misusing Image Tools**: Do not request account handle links via image tools. Type `@handle` + URL directly. Use `get_reference_image` strictly when generating new contextual images.
* **Unfiltered Searches**: Avoid `"find everything about X"`. Unbounded queries trigger rate limits and degrade retrieval quality.
* **Unnecessary Platform Blending**: Do not search across multiple platforms unless specifically conducting cross-platform comparisons.
* **Over-reliance on OCR**: OCR parsing can miss handwritten text or highly stylized typography.
* **Private/Deleted Content**: Deleted posts and private profiles are excluded from the index.
* **Caption-Only Geocoding**: Do not expect location filtering to resolve text mentions in captions unless the author applied a formal geotag.

### 5.4 Research Best Practices
1. **Chained Query Strategy**: Execute a `recency` search to gather current samples $\rightarrow$ Run `engagement` to locate originators $\rightarrow$ Enable `exclude_reposts: true` to trace spread networks.
2. **Negation Syntax**: Exclude unwanted parameters explicitly (e.g., `"Find videos without staff uniforms"` $\rightarrow$ append `-uniform` to `semantic_queries`).
3. **Signal Stacking**: Combine independent parameters to capture precise events (e.g., `"Yellow helmet + negative comments + last 3 days"`).
4. **Export Optimization**: Structure request as `"top 50 with links and created_at"` to receive data formatted for spreadsheet extraction.
5. **Source Validation**: Confirm original sources using `exclude_reposts: true` combined with `ranking_intent: "recency"`.

---

## 6. Quick Reference Cheat Sheet

| Intent / Target Filter | Recommended Query Construction | Inferred System Parameter |
| :--- | :--- | :--- |
| **Platform Target** | `"on Instagram / Reels only"` | `platform: "instagram"` |
| **High Engagement** | `"most viral / main / original / biggest / most shared"` | `ranking_intent: "engagement"` |
| **Temporal Recency** | `"new / latest / this week / today"` | `ranking_intent: "recency"` + `since` |
| **Informational Context** | `"why / explain / tutorial"` | `ranking_intent: "informational"` |
| **Exact Spoken/On-Screen Text** | `"exact phrase in video"` or Chinese characters | `semantic_queries` (OCR + Transcript boost) |
| **Visual Elements** | `"3 girls / yellow helmet / white shirt"` | `visual_tags` |
| **Comment Insights** | `"what are comments saying"` | `comment_summary` |
| **Geographic Tag** | `"in [city]"` | `location: "[city]"` |
| **Language Isolation** | `"Chinese posts only"` | `language: "zh-CN"` |
| **Hashtag Filtering** | `"with #boba tag"` | `hashtags: ["#boba"]` |
| **Account Type** | `"from verified accounts"` | `account_type: "verified"` |
| **Engagement Minimum** | `"over 10k likes"` | `min_engagement: { "likes": 10000 }` |
| **Deduplication** | `"original only, no reposts"` | `exclude_reposts: true` |
| **Media Format** | `"Reels only"` | `media_type: "reel"` |
| **Audio Template** | `"using the Nai Nai De Cha sound"` | `audio_id` lookup |
| **Video Duration** | `"under 30 seconds"` | `duration_range: { "max": 30 }` |

---

## 7. Version History

* **v1.0**: Initial release.
* **v1.1**: Added parameter support for `language`, `hashtags`, `account_type`, `min_engagement`, `exclude_reposts`, `media_type`, `audio_id`, and `duration_range`.
* **v1.2**: Added UTC timezone offsets, Content Reuse policy guardrails, and system error responses.
* **v1.3**: Added developer telemetry modes, archivist specifications, and dragnet workflows.
