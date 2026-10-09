---
name: buy-box-ranking
description: "Turn a researched company list into a ranked list of decisions - PRIORITY, WATCH or PASS - by building a written rubric from the buy box, getting it approved before a single row is ranked, applying it identically to every row in a fixed order, then running a mandatory four-part audit that verifies PRIORITY signals at source and hunts for false negatives among the exclusions. Triggers on: rank the list, score my targets, prioritise these companies, which ones should I call first, rank against my buy box, score this CSV against my thesis, re-rank the list, audit the ranking."
---

# Ranking

Two hundred companies become a list of decisions. Three buckets, because a number
between 1 and 100 invites an argument about whether a 71 beats a 68 and tells
nobody what to do on Monday.

The output has to be inspectable: every bucket carries the rules that produced it,
and every run carries an audit.

**Read first:**
- `references/ranking-rubric.md` — the buckets, the order, the ten hard rules,
  the healthy distributions, the audit. This skill is an implementation of that
  file
- `references/estimation-rules.md` — what an estimate is allowed to do
- `references/signal-evidence-rules.md` — what a signal strength means
- `BUY-BOX.md` — all of it

---

## Step 0 — Preconditions

1. `BUY-BOX.md` exists. No box, no ranking — you would be inventing a mandate,
   and an invented mandate ranks confidently
2. **Has the box changed since the last rubric was built?** If yes, hard rule 10
   applies and the whole list re-ranks. Say so before starting
3. **Is `ownership_type` filled?** If it is blank across many rows, stop and send
   them back to `buy-box-ownership-and-size`. Ownership gates ranking, and
   ranking without it produces a list you have to rank again
4. Signals pass has run, or the user has explicitly accepted ranking on fit alone
   — in which case say that no row can be PRIORITY, because PRIORITY requires a
   signal

---

## Step 1 — Build the rubric and get it approved

**Before a single row is ranked.** Write it out in full: every criterion, the buy
box section it came from, the test, and the bucket effect.

```
RUBRIC — commercial contract-recurring mechanical, 2026-10-09
Built from BUY-BOX.md last updated 2026-10-09

HARD EXCLUSIONS (any hit → PASS)
  E1  Residential, firearms, tobacco, payday lending, consumer
      collections                                            §8
  E2  On the portfolio conflict list (3 companies)            §8
  E3  On the already-worked list (11 companies)               §8
  E4  On the do-not-contact list (4 companies) — permanent    §8
  E5  Active OSHA enforcement, or bankruptcy within 5 years   §9

OWNERSHIP GATE
  O1  sponsor-backed → PASS ownership, always                 rule 2
  O2  public → PASS ownership                                 §7
  O3  corporate-subsidiary → in scope for platform only       §7
  O4  Not found → carries, capped at WATCH                    rule 4

GEOGRAPHY GATE
  G1  Outside IN / MI / OH / W-PA / N-KY → PASS geography     §5
  G2  CA, NY, NJ, coastal → PASS geography                    §5
  G3  add-on role requires ≤150 miles of Columbus OH or
      Grand Rapids MI                                         §5

SEGMENT AND MODEL GATE
  S1  Residential, new-build contracting, fire protection
      → PASS strategic                                        §4
  S2  Contract revenue below 40% of total, where evidenced
      → PASS strategic                                        §4
  S3  Single customer above 20% of revenue, where evidenced
      → PASS strategic                                        §4

SIZE BOX
  Z1  Verified revenue outside $8-45M → PASS economics        rule 7
  Z2  Estimate midpoint outside the box → WATCH, never PASS   rule 7
  Z3  Not found revenue → not a failed test, WATCH            rule 3
  Z4  EBITDA floor $1.5M, soft to $1.2M for a clean add-on    §3

ROLE
  R1  fit_role must be platform, add-on or either             rubric
  R2  add-on requires a named receiving platform and the
      adjacency stated                                         §2
  R3  Not found → capped at WATCH                             rubric

MUST-HAVES (all four required for PRIORITY)
  M1  Contract or recurring revenue above 40%, evidenced
      rather than described                                   §6
  M2  A named second-tier manager, not the owner and not
      the owner's child                                       §6
  M3  15+ years under substantially the same ownership        §6
  M4  Current state licence for the mechanical work performed §6

TIMING
  T1  PRIORITY requires signal_strength high or medium        rubric
  T2  low or Not found, everything else clean → WATCH         rubric
  T3  A signal never promotes an out-of-mandate company       rule 6

STANDING RULE
  X1  §11 — a company whose owner is under 50 with children
      in the business is WATCH permanently, whatever the
      growth signal says                                      §11
```

### 🚧 HARD GATE — approve the rubric

Show it in full and ask about these four specifically, because they are the ones
most often wrong and correcting them here saves a full rebuild:

1. **The exclusion list and the sponsor screen.** Is anything missing?
2. **Should `Not found` revenue really be non-fatal?** It should. Confirm the
   user agrees, because it is counter-intuitive
3. **Should a labeled estimate really never produce a PASS?** It should not.
   Same reason
4. **Are the must-haves really all required for PRIORITY?** Four is already a lot.
   If one is aspirational rather than required, demote it now

Get approval. **Then** rank.

---

## Step 2 — Rank every row in the same order

Always this order. Running size before ownership wastes work; running must-haves
before the gates wastes more.

1. Hard exclusions
2. Ownership gate
3. Geography gate
4. Segment and model gate
5. Size box
6. Role
7. Must-haves
8. Timing
9. Bucket
10. `fit_reason`

Write `fit_reason` naming the rules that fired, not a narrative:

```
PRIORITY — clean on E1-E5; founder-owned Tier 1 (O-pass); geography IN
(G1-pass); contract revenue 55% evidenced in 2026-06 trade press (M1);
estimate midpoint $20.5M inside box (Z2); platform role, named GM and
service manager (R1, M2); 32 years same ownership (M3); licence current
(M4); leadership signal high, 4 months old (T1)
```

```
WATCH — fit clean on all gates and all four must-haves; estimate midpoint
$9.2M inside box at medium confidence; add-on → Lakeside, 88 miles (R2);
no signal found at any tier (T2)
```

```
PASS — economics. Filed accounts FY2025 show £4.1M revenue, verified,
below the $8M floor (Z1). Everything else was clean.
```

A bucket with no `fit_reason` is a guess wearing a label. Hard rule 1.

---

## Step 3 — Run the audit, every time

Including when the numbers look fine. Four parts.

**1. Verify 10 PRIORITY signals at source.** Open the `signal_source` URL and
confirm the quoted words actually appear on the page. Report every one that does
not. This is the single most important thing the audit does: it is the check that
catches a fabricated or stale quote before it reaches an owner.

**2. Pull 20 random PASS rows and hunt for false negatives.** Not the ones you
remember — random. If any look obviously good, the filter is too tight. Report
them by name.

**3. Re-screen the keep pile against sponsors and the exclusion list.** Anything
that hits was missed upstream, or was acquired since capture.

**4. Sanity check the distribution** against the healthy bands: PRIORITY 5-15
percent, WATCH 30-50, PASS 30-50.

**Report the audit whether or not it is clean.** An audit that is never reported
is an audit that never ran. An audit that catches nothing on a 200-row list has
usually not run properly.

Apply every correction the audit produces, in the direction the rubric requires,
and report the net.

---

## Step 4 — Save the rubric

Write it to `rubric-[segment]-[date].md`.

A ranking nobody can argue with later is a ranking nobody can trust later. The
saved rubric is what makes "why is this a PASS" answerable in March.

---

## Step 5 — Report

```
RANKING COMPLETE — 198 rows, rubric-commercial-mechanical-2026-10-09.md

PRIORITY    14   ( 7%)
WATCH       79   (40%)
PASS       105   (53%)
Distribution inside the healthy band.

WHY ROWS DID NOT MAKE PRIORITY
  fits, no signal found                     41
  fits, signal below recency window          9
  fits, signal strength low                  8
  ownership Not found                       11
  revenue Not found, nothing contradicts     6
  edge of size box on an estimate            3
  role neither clean platform nor add-on     1

EXCLUSIONS THAT FIRED
  ownership    38   (23 sponsor — 9 still marketing as family owned,
                     11 corporate subsidiary, 4 public)
  strategic    31   (19 segment, 7 portfolio conflict, 5 already worked)
  economics    24   (verified figures only: 16 below floor, 8 above)
  geography    12

AUDIT
  1. PRIORITY signals verified          10 checked, 9 confirmed at URL
       1 failure: Mansell Mechanical, page rewritten since capture.
       Signal → Not found, row → WATCH.
  2. False negatives among PASS         20 pulled, 2 corrected
       Barrow Air Systems — excluded on a low-confidence $7.4M estimate
       against an $8M floor. Rule 7 says WATCH. Corrected.
       Dalemount Services — excluded on geography at 148 miles, inside
       the 150 mile add-on radius. Corrected.
  3. Keep pile re-screened              93 rows, 1 new sponsor hit
       Vennor Mechanical, acquired 2026-09 after capture. → PASS.
  4. Distribution                       inside band

NET AFTER AUDIT    PRIORITY 13, WATCH 82, PASS 103

The 13 PRIORITY rows are in targets.csv with a NOT KNOWN block on each.
Rubric saved. Re-run this skill if the buy box changes — rule 10.
```

---

## Notes

- **Never move a row to make the distribution look better.** Hard rule 9. If the
  distribution is implausible — 40 percent PRIORITY, or 5 percent surviving — say
  so and stop rather than handing over a list that flatters the user
- **When torn, choose the more generous bucket.** PRIORITY over nothing, WATCH
  over PASS. The expensive error is deleting a real target on thin information
- **A PASS is a decision, not a deletion.** Rows stay with the rule that excluded
  them, so the same company is not rediscovered and re-researched in six months
- **Any rubric change re-ranks the whole list.** A list ranked under two rubrics
  is two lists interleaved and nobody downstream can tell which is which
- **Write a `NOT KNOWN` block on every PRIORITY row.** What is still unknown and
  material: margin basis, customer concentration, whether second-tier management
  would stay. It is the difference between a brief and a sales pitch to yourself
- **This is where the package stops.** Contact details, outreach and pipeline are
  deliberately not here. Different job, different rules, and doing it badly is
  worse than not doing it
