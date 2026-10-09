---
name: buy-box-signals
description: "Find the dated, sourced, quotable reason to call a company this quarter rather than some other quarter - across the four families of growth, hiring, financing and leadership - quoted verbatim with a working URL, aged against a per-family recency window, and rated honestly including Not found. Triggers on: find the timing signals, why call them now, succession signals, is the owner retiring, hiring signals, new financing, growth signals, trigger events, what changed at this company."
---

# Timing Signals

Fit says a company belongs in the mandate. A signal says why this quarter. The
ranking rubric keeps them separate and PRIORITY requires both.

A signal is only a signal if it is **quoted verbatim, sourced to a working URL,
dated, and rated honestly.** Everything else is a feeling about a company, and a
feeling cannot be quoted back to an owner.

**Read first:**
- `references/signal-evidence-rules.md` — the four families, the evidence tiers,
  the strength ratings, the recency windows. This skill is an implementation of
  that file
- `references/ranking-rubric.md` — hard rule 6
- `BUY-BOX.md` section 9 — the user's own family ranking and any sector-specific
  signal they want watched

---

## Step 0 — Preconditions

1. Ownership is classified. A signal on a company a sponsor already owns is
   wasted research
2. Scope: rows with `verdict` blank and `signal` blank
3. Read buy box §9. Work the families in the user's priority order, so that if
   the batch runs long the most valuable family is already done
4. Batch 20 to 30

---

## Step 1 — Work the four families

### Growth
New site, depot, plant or region. Capacity added: fleet, lines, bays, beds,
machines. A named large contract or framework award. Headcount up materially
against a stated earlier number. A new service line or licence category.

### Hiring
First CFO, finance director or controller. First COO, GM or operations director.
A corporate development, integration or M&A role. A step change in open-role
volume. Senior roles in a new geography.

### Financing
New debt facility or refinancing, new lender of record. Minority or growth
investment. Sale-leaseback or property release. New UCC filings. A grant, bond or
public financing package.

### Leadership
Owner stating age, succession, retirement, or no next generation. Founder moving
to chair. A non-family CEO appointed. Death, illness or departure in the
ownership group. Second generation taking over, or declining to. A partner or
shareholder exit.

**Where to look, in order:** the company's own site and news page, their own
LinkedIn posts, trade press for the segment, local business journals, licence and
registry changes, UCC filings, procurement award notices, job boards.

Registry and filing changes are the most under-worked signal source in
origination, and they are Tier 1.

---

## Step 2 — Quote it

**Quote the words. Never paraphrase into quotation marks.**

If the source says "we are exploring options for the next phase", that is the
quote. Writing "the founder is looking to sell" is a fabrication, and it is the
kind of fabrication that ends up in an email to the founder.

```
signal:        "I'm 63. My daughter's a physician and my son has no interest
               in the trade. At some point this business needs an owner who
               isn't me."
signal_family: leadership
signal_source: https://example-tradepress.test/northline-mechanical-30
evidence_date: 2026-06-14
evidence_tier: 2
```

Where there is no quotable sentence — a UCC filing, a licence change — state the
fact flatly and cite the record:

```
signal:        New UCC-1 filed 2026-05-20, secured party Granite Ridge
               Credit, $6.5M. No prior facility of record since 2019.
signal_family: financing
signal_source: [state UCC search url]
evidence_date: 2026-05-20
evidence_tier: 1
```

---

## Step 3 — Age it

Against the family, not a single global cutoff.

| Family | Window | After that |
|---|---|---|
| Hiring | 90 days | Expired. A six-month-old job posting is a vacancy that was probably filled |
| Financing | 12 months | Downgrade one level |
| Growth | 12 months | Downgrade one level |
| Leadership | 24 months | Still usable. Succession moves slowly |

A signal with no date is `Not found`. Not `low` — `Not found`.

---

## Step 4 — Rate it

| `signal_strength` | Test |
|---|---|
| **high** | Tier 1 or 2, inside the window, about a decision rather than an atmosphere. Quotable to the owner without embarrassment |
| **medium** | Tier 1 to 3, inside the window, real but indirect. A first CFO hire with no stated reason sits here |
| **low** | Inside the window but thin: one job posting, a small headcount move, a vague quote |
| `Not found` | Nothing sourced and dated |

**One signal per row, the best one.** Extras go in `notes`. A row with five weak
signals is still a weak row, and stacking them is how a WATCH becomes a PRIORITY
it has not earned.

---

## Step 5 — Write back

Fill `signal`, `signal_family`, `signal_source`, `evidence_date`,
`signal_strength`, and update `evidence_tier` if the signal evidence is stronger
than the ownership evidence already recorded.

**This skill never writes `verdict`.** It supplies the timing input. The bucket
belongs to `buy-box-ranking`.

### 🚧 HARD GATE — before writing

Show:

- The strength distribution, and the `Not found` count stated plainly
- The family distribution against the user's §9 priority order
- **Every `high` signal in full** — the quote, the URL, the date. These are the
  rows that will become PRIORITY, and this is the cheapest moment to catch a bad
  one
- Every signal where the date is outside its window and what you did about it
- Any row where you found something interesting but unquotable, and why it did
  not make the cut

Get approval. Then write.

---

## Step 6 — Report

```
SIGNALS COMPLETE — 157 rows

high              19   (12%)
medium            34   (22%)
low               23   (15%)
Not found         81   (52%)   ← the normal and correct majority

By family (user priority: leadership 1, growth 2, hiring 2, financing 3)
  leadership      26   ← 11 high. Best family for this mandate, as expected
  growth          21   ←  4 high
  hiring          19   ←  2 high. 7 more found but outside the 90-day window
  financing       10   ←  2 high
  (rows may carry one signal only; 76 carry none)

Evidence tiers on the signals found
  Tier 1          22   (registry, UCC, award notices)
  Tier 2          38   (company or person on the record)
  Tier 3          16   (dated third-party naming its source)
  Tier 4           0   (not usable, 14 discarded)

Expired or downgraded
  7 hiring signals older than 90 days      → Not found
  4 growth signals 12-18 months old        → downgraded one level
  3 financing signals 13-16 months old     → downgraded one level

Sector-specific watch from §9
  First controls technician hire: found at 6 companies, 4 inside window.
  Loss of manufacturer dealer authorisation: none found.

Next: buy-box-ranking. The 81 Not found rows rank on fit alone and will
land at WATCH if the fit is clean. That is the correct outcome, not a gap.
```

---

## Notes

- **`Not found` on half the list or more is the expected result.** A list where
  every row has a signal has invented some. The 52 percent above is a healthy
  number, not a failure
- **Never infer succession from age alone.** A founder being 64 is not a signal.
  A founder saying there is nobody in the family to take it on is
- **Never infer intent from a website refresh, a new logo, or a tidy-looking
  set of accounts.** Those are the signals people invent when they cannot find
  real ones
- **A signal never changes the fit verdict**, only the timing verdict. Hard rule
  6 exists because a loud signal on an out-of-mandate company is the most
  seductive bad row on any list
- **Public sources only.** Anything behind a login that forbids scraping,
  anything paywalled without a licence, and anything requiring you to misrepresent
  who you are is out
- **Re-read signals quarterly.** Hiring signals expire in 90 days, which means a
  list ranked six months ago has a stale timing column even if the fit column is
  still correct
