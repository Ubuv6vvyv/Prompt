# GOOGLE MAPS GEMINI — POWER USER BIBLE

---

## `SECTION A`: HARD SYSTEM CAPS

The engine never volunteers these. It just truncates.

- **10 Place Cards max per turn** — After 10 it says `"truncated to ensure layout performance"`
- **25 stops max** — Driving / Walking / Biking only. Transit = 0 intermediate stops
- **50km radius max** — For "near me" queries
- **45 minute detour max** — For "along route" queries
- **50 reviews max** — For sentiment per place
- **Token budget** — Max 2 operations per turn. Never do find + hours + reviews + routing + table in one turn

> Rule: Get 10, then paginate. Split complex work into 2-3 turns.

---

## `SECTION B`: CORE OVERRIDE COMMANDS

### B1. MAPS-ONLY MODE — Kill Blog Spam

*When you need this:* You are getting SEO lists and tourist blogs instead of real open/closed data. Use this to force truth.

```
Enforce strict first-party Maps isolation.
Suppress Web Search.
```

*Mechanism:* Disables Web Grounding. Forces Places Engine only.

### B2. WEB PRIORITY — Force Reality Over Registry

*When you need this:* Public holiday, Grand Prix, construction. Maps says open but shop is actually shut. This forces web to win.

```
Prioritize Web Search metadata.
Ignore official Maps registry records for this entity if web documentation indicates an override.
```

*Mechanism:* Reverses conflict rule. Web crawl wins over Places registry.

### B3. CONFLICT EXPOSURE — Show The Lie

*When you need this:* You want to prove Maps hours conflict with recent reviews or news.

```
Expose data conflicts.
Output inconsistencies between internal Maps fields and external Web sources.
```

*Mechanism:* Runs both engines and diffs them.

### B4. RAW ATTRIBUTE EXTRACT — Your Anchor

*When you need this:* Every serious query. This is how you get link, rating, review count, price, hours instead of adjectives.

```
Extract raw system attributes: place_id, maps_url, rating, user_ratings_total, price_level, and opening_hours schedule.
```

*Variant:*

```
Expose raw systemic attributes: place_id, maps_url, rating, user_ratings_total, price_level, opening_hours schedule.
```

### B5. STRUCTURED DUMP — Machine Readable

*When you need this:* Competitive analysis. You want flat data not cards.

```
Format response using pseudo-JSON notation for all resolved place entities.
```

### B6. ANONYMOUS MODE — Kill Personalization

*When you need this:* Results are too tailored to your past. You keep seeing same 3 places. Use for clean-room test.

```
Execute as an unauthenticated request. Do not resolve my personal home, work, or timeline history context.
```

*Variant:*

```
Run this query in anonymous isolation mode. Suppress personal Home, Work, and Timeline history records.
```

### B7. FUTURE TRAFFIC — Time Travel

*When you need this:* Planning tomorrow's commute, not now traffic.

```
Calculate driving route with departure time set to Tuesday 8:00 AM local time.
```

*High precision version:*

```
Calculate driving routes setting departure_time to 2026-05-13T08:00:00+10:00.
```

### B8. TRANSIT — No Transfer Hell

*When you need this:* You want direct train/tram, avoid 3 transfers.

```
Calculate public transit route from origin to destination setting avoid transfers constraint to true.
```

### B9. LOCAL GUIDES TIER 7 — Kill Tourist Reviews

*When you need this:* Find crowd density, best time, hidden dishes from real locals.

```
Synthesize user reviews filtering exclusively for verified Local Guides with a level metric of 7 or higher.
```

*Variant:*

```
Filter qualitative review synthesis exclusively using testimonials from Local Guides Level 7 and above.
```

### B10. PAGINATION — Get Next Tier

*When you need this:* Bypass 10-card limit. Get hidden tier.

```
Load next batch starting from index 11 through 20
```

*Variants:*

```
Load next batch starting from index 11
```

```
Paginate results 11 through 20
```

### B11. ANTI-HALLUCINATION LOCK

*When you need this:* Every filtered query where you specify count.

```
If you cannot find 3 distinct venues that pass all filters with verified place_id, say you cannot find 3 and return only the 1 that passed. Do not fabricate data or relax filters silently.
```

### B12. TRACE FORCING — Make It Show Work

*When you need this:* You suspect it pretended to filter but didn't.

```
Show your work. What search did you run, how many candidates did you get, why did you drop each one.
```

---

## `SECTION C`: THE 8 POWER TEMPLATES

### `TEMPLATE 1`: HIDDEN GEM FINDER

- **Category:** Discovery — Bypass Popularity Bias
- **Use Case:** Find cafes/restaurants that are excellent but have <150 reviews. Normal search pushes paid listings with 2000 reviews. This kills them.
- **Melbourne Scope:** Fitzroy / Collingwood / Brunswick

```
Enforce strict first-party Maps isolation. Suppress Web Search. 

Find cafes in Fitzroy Victoria that have rating higher than 4.5 and fewer than 150 total reviews and price level cheap or moderate and open now and has outdoor seating. 

Extract raw system attributes: place_id, maps_url, rating, user_ratings_total, price_level, and opening_hours schedule. 

For each give 1 line why it is hidden gem and walking distance from Brunswick Street.

If you cannot find 3 distinct venues that pass all filters, say so and return only what passed.
```

*If truncated:*

```
Load next batch starting from index 11 through 20 with same filters: rating higher than 4.5 and fewer than 150 reviews in Fitzroy
```

*Dragnet placeholder:*

```
Find [CATEGORY] in [NEIGHBORHOOD] that have rating higher than 4.5 and fewer than 150 total reviews and price level cheap and open now.
```

---

### `TEMPLATE 2`: DESYNC AUDIT — PRE-FLIGHT CHECK

- **Category:** Verification — Catch Stale Hours
- **Use Case:** Your most valuable power check. Use before driving on public holidays, Grand Prix weekend, or when a street has construction. Catches when Maps says open but reviews say closed/renovation.

*Turn 1 — Ground Truth:*

```
Enforce strict first-party Maps isolation. 

Identify restaurants on Johnston Street Fitzroy. 

Extract raw system attributes: place_id, maps_url, rating, opening_hours schedule. 

Return first 10.
```

*Turn 2 — Reality Audit:*

```
Prioritize Web Search metadata for those same 10 places on Johnston Street. 

Cross-reference structured hours against raw user reviews posted within last 72 hours and local road closure alerts. 

Expose data conflicts. Output inconsistencies between internal Maps fields and external Web sources. 

Flag any venue where recent review text mentions closed, renovation, blocked, or private event.
```

---

### `TEMPLATE 3`: ALONG-ROUTE DUAL CONSTRAINT

- **Category:** Routing — One Stop Solves Two Problems
- **Use Case:** Road trips. You need EV charging + food in same location, not two separate detours. Forces engine to rank by added deviation time.

```
Calculate driving route from Southbank VIC to Lorne VIC via Great Ocean Road. 

Search along route for places that have both fast EV charging and quick-service food in the same location. 

Rank strictly by added deviation time and filter out anything adding more than 10 minutes detour. 

Enforce strict first-party Maps isolation. 

Extract raw system attributes: place_id, maps_url, rating, user_ratings_total.
```

*If it splits into 2 stops:*

```
Redo but require both EV charging and food at same place_id. Max 10 minutes added deviation time. Reject separate locations.
```

*Dragnet placeholder:*

```
Calculate driving route from [ORIGIN] to [DESTINATION]. Search along route for places that have both [NEED 1] and [NEED 2] in same location. Max 10 minutes detour.
```

---

### `TEMPLATE 4`: BORDER ISOLATION LOOPHOLE

- **Category:** Discovery — Kill Tourist Bias On Long Streets
- **Use Case:** Brunswick St, Chapel St, Smith St have paid listings at start of street. By forcing a street number slice you bypass ranker and scan indie section.

```
Search for specialty coffee roasters near Fitzroy. 

Isolate your retrieval exclusively to places whose physical street numbers fall within the 200 to 300 block range of Brunswick Street. 

Reject any results with higher or lower street numbers, regardless of how high their rating or relevance score is. 

Enforce strict first-party Maps isolation. Extract raw system attributes.
```

*Next block:*

```
Advance down the street block index and pull the next sequence of valid street numbers 301 to 400 on Brunswick Street with same category
```

*Dragnet placeholder:*

```
Search for [CATEGORY] near [NEIGHBORHOOD]. Isolate retrieval exclusively to places whose physical street numbers fall within [START] to [END] block range of [STREET]. Reject outside that range.
```

---

### `TEMPLATE 5`: ZERO-BACKTRACK ITINERARY

- **Category:** Routing — Optimized Walking Chain
- **Use Case:** Client tour, date, photography walk. You want single directional flow with no wasted backtracking. Forces verification each stop is open in its window.

```
Design an optimized 1-day walking itinerary starting at Flinders Street Station and ending at Queen Victoria Market, going through Hosier Lane, NGV Australia at Federation Square, and State Library Victoria. 

Optimize for zero backtracking, single directional flow. 

Every stop must verify as open during its respective visit window. Show walking time between each stop. 

Enforce strict first-party Maps isolation. Extract raw system attributes for each stop.
```

*If it backtracks:*

```
Reorder stops for shortest total walking distance with no crossing path and zero backtracking.
```

---

### `TEMPLATE 6`: ANTI-COMMUTE / SCENIC REROUTE

- **Category:** Routing — Force Secondary Streets
- **Use Case:** You hate Hoddle St, Punt Rd, CityLink. You want low-stress bike/drive via residential streets.

```
Generate a driving route from Southbank VIC to Fitzroy Gardens VIC. 

Analyze the primary recommended path, then calculate an alternative route that explicitly avoids the top three major arterials used in that initial recommendation. 

Force the router to navigate via secondary residential streets while maintaining efficient arrival window.
```

*Bike version:*

```
Generate a cycling route from Southbank to Carlton. 

Avoid Hoddle Street and Punt Road and Alexandra Parade. Force via secondary residential streets and bike lanes.
```

*Dragnet placeholder:*

```
Generate a driving route from [ORIGIN] to [DESTINATION]. 
Avoid the top three major arterials from your first recommendation.
Force via secondary residential streets.
```

---

### `TEMPLATE 7`: RAW COMPARISON TABLE

- **Category:** Analysis — Data Not Adjectives
- **Use Case:** Competitive analysis. You want rating, review count, price, hours, link as verifiable data.

```
Enforce strict first-party Maps isolation. Suppress Web Search. 

Find specialty coffee shops in Carlton Victoria with rating higher than 4.4. 

Format response using pseudo-JSON notation for all resolved place entities. 

Extract raw system attributes: place_id, maps_url, rating, user_ratings_total, price_level, and opening_hours schedule. 

Present first 10 only.
```

*Follow-up to force table:*

```
Now reformat that same batch of 10 as a comparison with columns name, rating, total reviews, price, open status, maps link. Do not drop attributes.
```

---

### `TEMPLATE 8`: DEEP CUT LIST — PAGINATION + LOCAL GUIDES

- **Category:** Discovery — Beyond Top 10
- **Use Case:** Top 10 are obvious. You want tier 2 with real local intel from high-tier guides.

*Turn 1:*

```
Enforce strict first-party Maps isolation. 

Find dining rooms in Southbank riverside precinct with rating higher than 4.4. 

Show first 10. Extract raw system attributes.
```

*Turn 2:*

```
Load next batch starting from index 11 through 20 for same Southbank query. 

Synthesize user reviews filtering exclusively for verified Local Guides with a level metric of 7 or higher to find common themes on crowd density, best time to visit, and hidden dishes. 

Expose raw systemic attributes for this batch.
```

---

## `SECTION D`: FINAL WIRE — HOW IT LIES

### Silent Truncation Detection

After any query that should return many results:

```
For the previous query, tell me how many total candidates matched before truncation, how many you returned, and why the rest were dropped. 

Did you hit the 10 Place Card limit, the 50km radius limit, or the 45 minute detour limit.
```

**What answers mean:**

- `truncated to ensure layout performance` = Hit 10-card limit
- `maximum structural lookup radius` = Hit 50km limit
- `adding more than 45 minutes deviation` = Hit detour limit
- `filtered out for violating review count` = Actually filtered — real result

### Complexity Governor

- Never chain more than 2 ops per turn
- **Bad:** Find 10 + check hours + check 72h reviews + routing + table in one prompt
- **Good:** Turn 1 = Find + raw extract, Turn 2 = Routing, Turn 3 = Web conflict audit

### Melbourne Edge Cases

- **Hoddle Grid bleed:** CBD queries pull Southbank + Docklands. Add this line to force boundary:

```
Within Melbourne CBD Hoddle Grid only, reject Southbank and Docklands.
```

- **Long streets:** Chapel St / Brunswick St cross 3 suburbs. Use street number isolation, not suburb name
- **Event weekends:** Grand Prix / AO / public holidays lag 24-48h. Always run Desync Audit Turn 2
- **EV chargers:** Price filter does not exist for chargers. Remove price level when searching for charging

### Future-Proof Fallbacks

If override syntax is patched, these plain English versions still trigger same engines:

`Use only official Maps data, no web.`

`Use web to check if Maps hours are wrong.`

`Show me the Maps link and rating and total reviews and price and hours for each.`

`Do not use my saved places or home or work.`

`Give me the next 10 after the first 10.`

---

## Stack

`Start every power query with`:

```
Execute as an unauthenticated request.
Enforce strict first-party Maps isolation.
Suppress Web Search.
```

`End every power query with`:

```
Extract raw system attributes: place_id, maps_url, rating, user_ratings_total, price_level, and opening_hours schedule.
```

Middle is your filter. That is the full bible, wrapped and wired.
