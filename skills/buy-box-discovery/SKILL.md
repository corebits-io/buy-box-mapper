---
name: buy-box-discovery
description: "Enumerate the private companies inside a mapped segment from licence rosters, registries, association directories, exhibitor lists and dealer locators - the sources bought lists never cover - with a source string on every row, honest deduplication, and a coverage log that names what the pull missed. Triggers on: find the companies, enumerate the population, build the target list, who are the operators in this segment, pull the licence roster, find private companies matching my buy box."
---

# Company Discovery

This is the step that decides whether the list is proprietary. Everything after
it is processing.

A list pulled from an M&A database covers the companies that have been written
about, which is the same population every other fund is calling. The companies
that appear in a licence roster and in no aggregator are, disproportionately, the
ones nobody has phoned.

**Read first:**
- `market-map-[segment]-[date].md` — specifically the source list and the segment
  boundary
- `references/sourcing-directories.md`
- `BUY-BOX.md` sections 4, 5, 8

---

## Step 0 — Preconditions

1. **A market map exists for this segment and geography.** If not, stop and run
   `buy-box-market-map`. Discovery without a map pulls from whatever source is
   easiest and inherits its bias invisibly
2. The map's verdict is SOURCE IT or SOURCE A DIFFERENT SLICE. If it is DO NOT
   SOURCE IT, say so and stop
3. `targets.csv` exists with the 29 columns
4. Read the do-not-contact list and the already-worked list from buy box §8.
   These never enter the list as new rows

---

## Step 1 — Work the sources in tier order

Start with Tier 1. The spine of the list should be statutory or regulatory.

**Pull the whole segment, then filter.** Never search and cherry-pick. Searching
a roster for the names you recognise biases the list toward the well-marketed,
which is the exact opposite of the point.

For each source, record before you pull:

- What population it covers
- How you filtered (category, county, licence class, membership tier)
- What it capped or truncated
- How many rows came out

A 500-row export from a 1,200-row roster is a fact. Write it down.

---

## Step 2 — One row per company, with its source

Fill only these columns at this stage:

`company`, `domain`, `hq_location`, `country`, `sector`, `segment`,
`year_founded`, `employee_count`, `source`, `date_added`, `status` = `found`

The `source` string must be specific enough that somebody else could re-run the
pull:

```
Good:  Indiana mechanical contractor licence roster, HVAC category,
       Allen + Whitley + Huntington counties, complete pull 2026-10-02;
       cross-found in MCAA member directory and 2026 AHR exhibitor list

Bad:   licence roster
Bad:   web search
```

Leave everything else blank. Ownership, size, signals and ranking are later
skills with their own rules, and a half-guessed ownership field written here is
worse than an empty one.

---

## Step 3 — Cross-find

A company appearing in three independent sources is a real company. One
appearing in a single aggregator may be a duplicate, a defunct entity, or a
holding shell with no operations.

Append each additional source to the `source` string rather than overwriting it.
The cross-find is what makes the row credible, and losing it later is expensive.

---

## Step 4 — Deduplicate

Private company lists duplicate heavily and the duplicates are not obvious.

Merge on **domain** first, then **registry number**, then **normalised name plus
postcode**.

Watch for:

- Trading name versus registered name
- Holding company and operating subsidiary listed separately
- Branch offices appearing as separate companies in Maps and directories
- Entity suffix noise: Ltd, Limited, LLC, Inc, Inc., Corp, Co
- Hand-typed registry spelling variants

Keep the merged row. Put the other names in `notes`. **Keep every source
string.** A dedupe that silently drops a source string destroys the cross-find
evidence.

Report the dedupe count. A 312-row pull collapsing to 247 is normal and worth
seeing.

---

## Step 5 — Apply only the cheap gates

Two gates run here, because they are free and they stop downstream work on rows
that cannot survive.

**Geography.** Outside a hard geographic constraint in buy box §5 — mark
`verdict` = `PASS`, `excluded_by` = `geography`. The row stays on the list.

**Segment boundary.** Clearly outside the segment definition in the map — mark
`verdict` = `PASS`, `excluded_by` = `strategic`.

**Nothing else.** Do not apply the size box here: there are no revenue figures
yet, and excluding on headcount at this stage deletes companies whose headcount
is simply unrecorded. Do not apply ownership: that is a research step, not a
filter.

---

## Step 6 — The coverage log

Write it into the run file. It is the part that makes the list honest.

```
COVERAGE LOG

Sources worked
  Indiana contractor licence roster      complete pull, 1,412 rows
                                         filtered to HVAC + plumbing
                                         categories, 11 counties → 203
  Michigan licence roster                complete pull → 147
  Ohio licence roster                    CAPPED at 500 rows by the portal.
                                         Western Ohio counties only.
                                         ~180 estimated missing. ← gap
  MCAA member directory                  210 members, 68 in geography
  AHR exhibitor 2024/25/26               94 contractors, 31 in geography
  3 manufacturer dealer locators         77 in geography
  LinkedIn company search                headcount only, no new rows

Known gaps
  - Ohio roster truncation above. Rerun by county to close it.
  - Unlicensed adjacent services (controls-only integrators) are not on
    any roster. 9 found via dealer locators, likely incomplete.
  - Companies with no web presence and no association membership appear
    only in the rosters, so the Ohio gap is probably concentrated there.

Bias statement
  This list leans toward licensed operators, which is the segment
  definition, and toward association members and exhibitors, which
  over-represents larger and more growth-minded firms. The 40-year-old
  firm that joined nothing appears only via the rosters.
```

---

## Step 7 — Volume check

**100 to 300 well-qualified companies for a focused mandate.** Not thousands.

If the pull is under 60 rows: the geography is too narrow, a source capped, or
the map's population estimate was wrong. Name which.

If it is over 500: the segment boundary is loose. Tighten it rather than carrying
noise, because every row costs research time downstream and a bloated list buries
the dozen real conversations.

### 🚧 HARD GATE — before writing

Show:

- Row count by source, before and after dedupe
- The geography and segment PASS counts
- The full coverage log including every gap and the bias statement
- 15 sample rows, including at least 3 with a blank `domain` and 3 with a blank
  `employee_count`, so the user sees what thin rows look like
- Any row that looks like a duplicate you chose not to merge, and why

Get approval. Then write to `targets.csv`.

---

## Step 8 — Report

```
DISCOVERY COMPLETE — 2026-10-07

Enumerated            312 rows from 7 sources
After dedupe          247   (65 merges: 41 name variants, 14 branches,
                             10 holding/operating pairs)
Cross-found in 2+     118   (48%)
Single source only    129   ← 94 of these are roster-only, which is the
                             proprietary end of the list, not the weak end

Cheap gates
  PASS geography       37
  PASS segment         12
  Carried forward      198

Field completeness
  domain               171 / 198   (27 have no website at all)
  employee_count       134 / 198
  year_founded         188 / 198

Coverage gaps          Ohio roster capped at 500, ~180 rows likely missing.
                       Recommend a per-county rerun before ranking.

Next: buy-box-ownership-and-size on the 198 carried forward.
```

---

## Notes

- **27 companies with no website is a feature.** Hard rule 5 in the ranking
  rubric exists because those are frequently the best rows on the list
- **Never fabricate a domain.** If a company has no site, `domain` is blank. A
  guessed domain propagates into every later step
- **Never invent a headcount.** Blank beats a guess, and the sizing skill is
  built to handle blanks honestly
- **Report the cap, always.** A truncated source pull is the single most common
  silent failure in discovery, and it looks exactly like a complete one
- **Rows never get deleted.** A geography PASS stays on the list so the same
  company does not get rediscovered and re-researched next quarter
