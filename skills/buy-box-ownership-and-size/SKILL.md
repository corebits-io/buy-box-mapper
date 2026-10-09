---
name: buy-box-ownership-and-size
description: "Establish who actually owns each company from filings and registers, run the sponsor screen that catches companies already acquired but still marketing themselves as family owned, then produce a defensible revenue and EBITDA range for companies that publish nothing - always labeled as an estimate with the basis attached. Triggers on: who owns these companies, ownership research, sponsor screen, is this PE owned, establish ownership, estimate revenue, how big is this company, EBITDA estimate, size the targets, is this inside our size box."
---

# Ownership and Size

Two jobs in one pass, in this order, because the order saves work: establish
ownership first, then size only the rows that survived it. Estimating revenue for
a company a sponsor bought two years ago is wasted research.

**Read first:**
- `references/estimation-rules.md` — the methods, the labeling rule, the
  confidence ladder, and what an estimate is allowed to do to a ranking. The
  sizing half of this skill is an implementation of that file
- `references/ranking-rubric.md` — hard rules 2, 3, 4 and 7
- `market-map-[segment]-[date].md` — the consolidator list for the screen, and
  the segment economics every estimate depends on
- `BUY-BOX.md` sections 3, 7, 8

---

## Step 0 — Preconditions

1. Read the market map's segment economics. **If revenue per head and typical
   margin are both `Not found`, stop the sizing half and say so.** Every
   estimate depends on a sourced sector benchmark, and inventing one propagates a
   made-up number into every row, where they will all be wrong the same way
2. Read the consolidator list from the map. No list, no screen
3. Scope: rows in `targets.csv` with `verdict` blank
4. Batch 20 to 30 rows. Report between batches

---

# Part A — Ownership

## Step 1 — Classify from evidence, not from appearance

| `ownership_type` | What establishes it |
|---|---|
| `founder-owned` | Registry shows the same individual as officer or shareholder since formation, or close to it |
| `family-owned` | Shared surname across officers or shareholders across generations, or the company stating it with a date |
| `management-owned` | A share transfer to managers on record, no fund entity |
| `employee-owned` | ESOP filing, trust registration, or the company stating it |
| `sponsor-backed` | A fund entity in the shareholder register, a sponsor naming it as a platform or add-on, or a UCC filing naming a sponsor vehicle |
| `corporate-subsidiary` | A corporate parent on record |
| `public` | Listed, or a listed parent |
| `Not found` | No evidence either way. The honest answer, and common |

**A company calling itself family owned on its about page is Tier 3 evidence at
best.** Companies keep that language for years after a sale because it is good
marketing. Check the register.

Record `ownership_evidence` with the tier, the source, and the date:

```
Tier 1 — Indiana SOS filings list the same sole officer since 1994
incorporation; no share transfers on record. Cross-checked against about
page dated 2026-02.
```

Record `evidence_tier` as 1 to 4. See `references/signal-evidence-rules.md` for
the tier definitions.

## Step 2 — The sponsor screen

Runs on **every** row, including rows that look obviously founder-owned. This is
the most commonly skipped step in origination and the most embarrassing one to
get wrong out loud, in writing, to an owner who sold two years ago.

Four checks:

1. **The consolidator list from the map.** Is this company named as a platform or
   an add-on by any of them?
2. **Trade press, last 36 months.** Acquisition, investment, merger, "partners
   with", "joins", "backed by"
3. **UCC filings or equivalent security registrations.** A fund vehicle or a
   sponsor-affiliated lender as secured party is a strong tell
4. **The register itself.** Any corporate shareholder whose name does not look
   like a family holding company. Follow it one level up

Write the result to `sponsor_screen`:

```
clear — screened against the 5 sponsor platforms named in the market map,
no trade press 2023-2026, no UCC filings naming a fund entity

hit — acquired by Ridgeline Partners 2024-11, announced as an add-on to
their Meridian Mechanical platform [url]
```

**A hit is `verdict` = `PASS`, `excluded_by` = `ownership`.** Always. Whatever
the fit looks like otherwise.

Report the hits that still present themselves as family owned separately. That
list is the most valuable output of this step: each one is a letter that does not
get written.

## Step 3 — Ownership gate

- `sponsor-backed`, `public`, or an ownership type the buy box puts out of scope
  → `PASS`, `excluded_by` = `ownership`
- `Not found` → **not a PASS.** Carries forward and caps the row at WATCH per
  hard rule 4
- In scope → carries forward to sizing

---

# Part B — Size

Only on rows that survived the ownership gate.

## Step 4 — Separate verified from estimated

**Verified** means the company or a filing published it: statutory accounts, a
public contract award value, a dated on-the-record statement, a regulatory filing.

Everything else is an estimate. **An M&A database revenue field is an estimate
somebody else made.** One data point, named as the source, never promoted to
verification by repetition.

## Step 5 — At least two methods

Revenue per head, public comparables, capacity, contract awards, trade benchmark
tiers. The full method notes are in `references/estimation-rules.md`.

Where two methods disagree by more than about 40 percent: say so, widen the
range, drop the confidence. Do not pick the one you prefer.

## Step 6 — Write it with the label attached

Never this:

```
est_revenue: $12M
```

Always this:

```
est_revenue: $10-14M (estimate: 85 staff x $130-165k sector-typical revenue
             per head from MCAA 2025 regional survey; headcount from
             LinkedIn 2026-05, unverified. Cross-check: $11.2M floor implied
             by 2024 state contract awards.)
```

The label travels with the number. A stripped estimate becomes a fact the moment
somebody pastes it into a second document.

EBITDA is only ever a margin band applied to a revenue range, never a point, and
never a margin you cannot source.

## Step 7 — Confidence

`verified` / `high` / `medium` / `low` / `Not found`, per the ladder in the
estimation rules. Write it to `financial_confidence`. A range with no confidence
rating is a range nobody downstream can weigh.

## Step 8 — Decide the platform or add-on role

This is the question the ranking rubric will not let you leave blank.

| `fit_role` | Test, against buy box §2 and §3 |
|---|---|
| `platform` | Upper half of the size box, a named second-tier manager who is not the owner, systems that would survive a transition, a defensible position in its segment |
| `add-on` | Adjacency to a **named** existing platform from buy box §2, inside the stated radius, complementary rather than duplicated coverage |
| `either` | Genuinely both. Allowed, but name the platform the add-on case would attach to |
| `Not found` | Not enough known. Caps the row at WATCH |

Write `fit_role_reason` naming the evidence. For an add-on, name the receiving
platform and the adjacency:

```
add-on → Keystone Mechanical. 92 miles from Columbus, inside the 150 mile
radius. Controls capability Keystone currently subcontracts. No overlap in
named customers found.
```

"Add-on" with no platform and no adjacency is not an answer.

---

### 🚧 HARD GATE — before writing

Show:

- Ownership distribution, and the `evidence_tier` distribution with it
- **Every sponsor screen hit, named** — and separately, every hit that still
  markets itself as family owned
- How many rows are `verified` versus estimated on revenue. **If almost none are
  verified, say so plainly**, because the whole size gate is then resting on one
  benchmark
- **Every row whose estimate lands outside the size box**, since those become
  WATCH rather than PASS and the user may want to look at them individually
- Every case where two methods disagreed materially, with both figures
- The `fit_role` distribution, and every `either` with its reasoning
- 10 full sample rows including at least 2 `Not found` ownership and 2
  `Not found` revenue

Get approval. Then write.

---

## Step 9 — Report

```
OWNERSHIP AND SIZE COMPLETE — 198 rows

OWNERSHIP
  founder-owned          81   (Tier 1: 54, Tier 2: 27)
  family-owned           44   (Tier 1: 22, Tier 2: 19, Tier 3: 3)
  management-owned       11
  employee-owned          4
  sponsor-backed         23   → PASS ownership
  corporate-subsidiary   11   → PASS ownership (out of scope per §7)
  public                  4   → PASS ownership
  Not found              20   → carried, capped at WATCH

  Sponsor screen hits    23. Nine of them still describe themselves as
                         family owned on their own site. Named above.
                         Those nine are the reason this step exists.

  Surviving the gate    160

SIZE  (on the 160)
  verified               14   ( 9%)  ← 11 filed accounts, 3 contract values
  high                   38   (24%)
  medium                 61   (38%)
  low                    22   (14%)
  Not found              25   (16%)

  Methods used
    revenue per head    138   (headcount: 71 LinkedIn, 49 licence roster,
                               18 company site)
    capacity             44   (fleet size from licence records)
    contract awards      31   (floor only)
    comparables           7
    trade benchmark      19

  Against the size box ($8-45M revenue, $1.5M+ EBITDA)
    verified in box       11
    estimate midpoint in  94
    estimate outside      30   → WATCH, never PASS (rule 7)
         21 below floor   ← 13 of these are low confidence. Worth a look
                            before anybody writes them off
          9 above ceiling
    verified outside       3   → PASS economics
    Not found             25   → not a failed size test (rule 3)

  Method disagreements    7 rows over 40% apart. Ranges widened,
                          confidence dropped to low, all 7 listed above.

  Benchmark provenance    MCAA 2025 regional survey, $130-165k revenue per
                          head, 15-18% margin. Every estimate here rests on
                          this. If it is wrong, every row is wrong the same
                          way.

ROLE
  platform               29
  add-on                 88   (receiving platform named on all 88)
  either                 17
  Not found              26   → capped at WATCH

Next: buy-box-signals on the 157 still carrying forward.
```

---

## Notes

- **The asymmetry in rule 7 is deliberate.** A verified figure outside the box is
  a PASS; a labeled estimate outside the box is a WATCH. Excluding a real target
  because a headcount guess landed 15 percent under the floor is the most
  expensive routine error in origination, and it happens silently
- **This skill never writes `verdict` for a surviving row.** It writes PASS only
  for the ownership and economics gates it owns. The bucket belongs to
  `buy-box-ranking`, under an approved rubric, so the decision stays inspectable
- **Never estimate a valuation or a multiple.** Different discipline, and a wrong
  number there is worse than no number
- **Follow a corporate shareholder one level up, then stop.** Two levels of
  holding company research per row does not pay for itself at this stage. Record
  what you found and flag it
- **`Not found` ownership is not a research failure.** In some jurisdictions the
  information is simply not published, and saying so is the correct output
