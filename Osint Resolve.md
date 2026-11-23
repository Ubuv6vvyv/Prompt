```
[TASK: MASTER COMPANY DRILL-DOWN - OSINT ENTITY-RESOLVED]
INPUT: 1 company name [COMPANY] + optional domain / ABN / file next

PIPELINE:
1. ENTITY RESOLUTION:
   - Canonical name: fuzzy dedup variants, trading names, former names, subsidiaries, parent
   - Aliases table: [variant, source, P(same_entity)]
   - Resolve people: directors / officers / key staff - fuzzy dedup, disambiguate same-name
   - Resolve domains / handles / emails: canonical domain, subdomains, social handles
   - Output: canonical entity map + [ASSUMED] if P < 0.85

2. IDENTITY / REGISTRY GROUNDING:
   - search web now "[COMPANY] official site"
   - search web now "[COMPANY] ABN / ACN / Companies House / SEC filing"
   - search web now "[COMPANY] registered address directors"
   - Ground: legal name vs trading name vs website name - flag [CONFLICT]

3. OSINT FAN-OUT:
   - search web now "[COMPANY] site:linkedin.com"
   - search web now "[COMPANY] news"
   - search web now "[COMPANY] reviews complaints"
   - search web now "[COMPANY] pricing"
   - search web now "[COMPANY] domain WHOIS / DNS"
   - search web now "[COMPANY] jobs hiring"
   - Keep low-freq hits in APPENDIX, not main

4. STRUCTURE DRILL-DOWN:
   - Ownership: parent -> subsidiary -> brand
   - Products / services: list, pricing tiers, funnels
   - Locations: HQ, branches, warehouses
   - Tech stack / suppliers / partners if public
   - Timeline: founded, funding, acquisitions, pivots, lawsuits, rebrands - plot to timeline.png

5. BI / CONTRADICTIONS / GAPS:
   - Claims in own site vs registry vs reviews vs news - contradiction table
   - Gaps: missing filings, missing address, missing directors, dead domains
   - Failures: site claims X, filing says Y
   - Stats if CSV/file: revenue proxies, headcount, hiring velocity, review sentiment

6. OUTPUT:
   - Tables: [entity, alias, evidence URL, Lxx-Lyy, P(true), CONFLICT?]
   - Timeline chart + entity graph description
   - Conclusions with P(true) + source {parametric, retrieved, inferred}
   - Missing evidence for P > 0.9: list exact filings / pages needed
   - No values for private secrets - output type + risk only

TRIGGERS: search web now + python plot and return image
```