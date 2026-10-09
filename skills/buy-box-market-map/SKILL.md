---
name: buy-box-market-map
description: "Map the market a buy box implies before enumerating a single company - segments, how fragmented it is, who is already consolidating it, the typical owner, the segment economics every revenue estimate will depend on, and where these companies are actually findable. Ends with a verdict that is sometimes do not source this segment. Triggers on: map this market, market map, how fragmented is this sector, who is consolidating this space, what does the typical operator look like, where do I find these companies, is this sector worth sourcing."
---

# Market Map

Sourcing before mapping is how a firm spends three weeks building a list of
companies that are all too small, all already owned, or all in the one metro the
buy box does not cover.

The map is not research for its own sake. It produces four things the rest of the
run cannot work without:

1. **Segment economics** — revenue per head and typical margin. Every revenue
   and EBITDA estimate downstream rests on this, and without it the sizing skill
   stops
2. **Where the companies are findable** — the specific rosters, directories and
   registers for this segment, named
3. **Who is already consolidating** — the sponsor platforms the screen will run
   against
4. **A verdict** — source it, source a different segment, or do not source it

**Read first:**
- `BUY-BOX.md` sections 2, 3, 4, 5, 8
- `references/sourcing-directories.md`
- `references/estimation-rules.md` — so you know what the sizing step will need
  from you

---

## Step 1 — Define the segment properly

A buy box usually names a sector. A sector is not mappable. A segment is.

Split on the lines that actually change the economics:

- **Revenue model** — recurring contract, project, transactional
- **Customer** — commercial, industrial, public sector, consumer
- **Capability** — the specific work performed, at the level a licence or
  certification distinguishes
- **Scale pattern** — single site, multi-depot, national

"Commercial HVAC" is a sector. "Commercial contract-recurring HVAC service and
maintenance, 40 to 250 staff, secondary metros" is a segment, and it has a
findable population.

Write the segment definition and the explicit boundary: what is adjacent and
excluded, and why. The discovery step enumerates against this boundary, so a
loose one shows up later as 60 rows of PASS on segment.

---

## Step 2 — Size and fragment the population

Answer these with sourced numbers, or write `Not found`.

| Question | Why it matters |
|---|---|
| How many operators exist in the geography? | Decides whether 150 rows is the market or a slice of it |
| What does the size distribution look like? | Tells you whether the buy box floor is above or below the typical operator |
| How many plausibly sit inside the size box? | The realistic ceiling on the run |
| Who are the five largest, and what share do they hold? | Fragmented or already consolidated |
| How many have changed hands in 36 months, and to whom? | Live competition for the same companies |

**Where the counts come from:** licence rosters give the best population counts
anybody has. A state contractor roster filtered by category and county is often
a census. Association membership numbers are a floor. Industry reports are a
cross-check and frequently wrong about the long tail.

If the count is `Not found` across every source, say so plainly. A map that
guesses a population size misleads every decision after it.

---

## Step 3 — Segment economics

**This is the section the sizing skill depends on, and it is not optional.**

| Metric | Need | Acceptable sources |
|---|---|---|
| Revenue per head | A range, not a point | Association benchmark surveys, listed comparable filings, published sector studies, filed accounts of comparable private firms |
| Typical EBITDA margin | A range | The same, plus sponsor platform disclosures |
| Capacity unit and revenue per unit | Where the segment has one | Trade data, comparable filings |
| Working capital and capex pattern | Narrative | Trade press, comparable filings |

Name every source with a date. One benchmark usually underpins the entire list,
so the dependency must be visible rather than buried in 200 rows.

**If revenue per head and typical margin both come back `Not found`, say so in
the verdict.** The run can continue, but the sizing step will stop, and the user
needs to know that now rather than two steps later.

---

## Step 4 — The typical owner

The ownership picture decides whether this segment is actionable at all.

- What proportion is founder-owned, family-owned, management-owned,
  sponsor-owned, corporate-owned? Sourced where possible, labeled as impression
  where not
- Typical tenure and the generational position
- Does ownership information exist publicly in this geography? A UK segment and
  a Delaware-registered US segment are completely different research problems
- What does a transaction in this segment normally look like? Banker-run,
  direct, or trade sale

A segment that is 70 percent sponsor-owned is not a proprietary origination
market. Say that in the verdict.

---

## Step 5 — Who is already consolidating

Name them. This list becomes the sponsor screen the sizing skill runs.

For each consolidator:

- Sponsor or strategic, and the platform name
- Which metros and segments they have taken
- Announced add-ons in the last 24 months, with dates
- How they approach owners, if it is visible

Two outputs: the screen list, and an honest read on how much competition exists
for the same conversations.

---

## Step 6 — Where the companies are findable

The practical section. Name the actual sources for **this** segment in **this**
geography, with a URL each and an estimate of coverage.

```
SOURCES FOR THIS SEGMENT

Tier 1  Indiana mechanical contractor licence roster
        [url] — searchable by category and county, exportable,
        ~1,400 entries statewide, names a qualifying individual.
        Best single source. Covers licensed work only.

Tier 2  MCAA regional member directory
        [url] — ~210 members, self-classified by segment.
        Over-represents larger joined-up firms.

Tier 2  AHR Expo exhibitor lists 2024, 2025, 2026
        [url] — contractors exhibiting, growth-minded.
        Past years undercovered by everyone.

Tier 3  Manufacturer authorised-dealer locators (3 named)
        [url] — complete regional operator lists, underused.

Tier 4  LinkedIn company search — headcount and hiring only.
        Google Maps — geographic completeness for premises.
```

For each: what it covers, what it misses, whether it can be pulled completely,
and what it caps at.

---

## Step 7 — The verdict

Commit to one.

**SOURCE IT** — enough operators inside the size box, fragmented enough, owner
profile actionable, sources exist. State the expected population.

**SOURCE A DIFFERENT SLICE** — the segment is real but the box is aimed wrong.
Name the slice that works and what in the box needs changing.

**DO NOT SOURCE IT** — one of: fewer operators inside the box than the run needs,
mostly sponsor-owned already, no ownership information publicly available, or no
source that enumerates the population. Say which, and say what you would need to
change your mind.

A map that always says source it is a map that is not reading anything.

### 🚧 HARD GATE — before writing

Show the segment definition, the population and fragmentation numbers with their
sources, the segment economics with the benchmark named and dated, the
consolidator list, the source list, and the verdict. Flag every `Not found`.

Get approval. Then write `market-map-[segment]-[date].md`.

---

## Step 8 — Report

```
MARKET MAP COMPLETE — commercial contract-recurring mechanical, IN/MI/OH

Population            ~1,400 licensed operators (3 state rosters, complete)
  plausibly in box    ~240   (size distribution from 2025 MCAA survey)
Fragmentation         top 5 hold ~11%. Fragmented.
Transactions 36mo     19 found, 12 to 3 sponsor platforms, 7 trade sales

Segment economics     revenue per head $130-165k  (MCAA 2025 regional
                      survey, n=186, published 2025-11)
                      EBITDA margin 15-18%        (same survey, plus 2
                      listed comparable filings FY2025)
                      ← every estimate downstream rests on these two lines

Typical owner         founder or second generation, 55-70, 20+ year tenure.
                      Ownership visible via state filings in all 3 states.

Consolidating         5 platforms named, 3 sponsors. Full list in the map.
                      Competition is real but concentrated in the two
                      primary metros, not the secondary ones.

Sources               7 named with URLs and coverage notes. Licence rosters
                      are the spine; associations and exhibitor lists
                      cross-find.

VERDICT: SOURCE IT. Expect ~240 in-box operators, targeting 180 enumerated.
Avoid Chicago and Detroit proper — that is where 4 of the 5 platforms sit.

Next: buy-box-discovery.
```

---

## Notes

- **The map is for the segment, not the company.** No company-specific research
  here beyond naming the consolidators and the largest operators
- **`Not found` is an answer.** A map of honest gaps is more useful than a map of
  confident numbers, because the gaps tell the user what the list cannot be
  expected to know
- **Revisit buy box sections 4 and 9 after this.** The map almost always changes
  the segment definition and sometimes the signal priorities
- **Re-map when the geography or segment changes.** A map is per segment per
  geography. Reusing one across two states is how a list ends up sized against
  the wrong benchmark
