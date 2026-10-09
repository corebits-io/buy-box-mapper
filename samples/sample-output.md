# What a Finished Run Looks Like

> **Every company, person, quote, URL and number on this page is invented.** This
> is a shape, not data. It exists so you know what you are getting before you
> install anything.
>
> The run below is Harbour Ridge Partners against the worked buy box in
> `templates/BUY-BOX-example.md`: contract-recurring commercial mechanical
> services, secondary Midwest metros, founder-owned, $8-45M revenue.

---

## The run header

```
BUY BOX MAP COMPLETE — 2026-10-09
Mandate: Harbour Ridge Partners, commercial mechanical services, Midwest
Rubric: rubric-commercial-mechanical-2026-10-09.md (approved before scoring)

Population enumerated        312
  after dedupe               247
  after geography gate       198
  ranked                     198

PRIORITY    14   ( 7%)
WATCH       79   (40%)
PASS       105   (53%)

Distribution is inside the healthy band for a mapped mandate.
```

---

## The PRIORITY rows

Fourteen rows. Here are the first six as they appear in the summary table.

| # | Company | HQ | Segment | Rev est | EBITDA est | Owner | Role | Signal |
|---|---|---|---|---|---|---|---|---|
| 1 | Northline Mechanical | Fort Wayne, IN | Commercial HVAC service | $18-23M | $2.9-4.1M | Founder | platform | Founder, 63, stated no family successor (trade press, 2026-06-14) |
| 2 | Vallen Building Systems | Toledo, OH | HVAC service + controls | $12-15M | $1.8-2.7M | Family, 2nd gen | add-on → Keystone | First CFO hired (own announcement, 2026-08-02) |
| 3 | Crestmark Plumbing Services | Lansing, MI | Commercial plumbing service | $9-11M | $1.4-2.0M | Founder | add-on → Lakeside | New $6.5M credit facility, new lender of record (UCC, 2026-05-20) |
| 4 | Ridgeway Refrigeration | South Bend, IN | Cold storage refrigeration | $14-18M | $2.4-3.4M | Management-owned | platform | Two of four shareholders exited (register, 2026-03-11) |
| 5 | Allenby Mechanical Group | Erie, PA | HVAC service | $10-13M | $1.5-2.3M | Founder | add-on → Keystone | Third depot opened, 22 roles posted (own site, 2026-07-30) |
| 6 | Trent Valley Controls | Kalamazoo, MI | Building automation | $8-10M | $1.3-1.9M | Founder | add-on → Lakeside | Founder moved to chair, non-family MD appointed (register, 2026-04-08) |

Six of the fourteen are add-ons with the receiving platform named. That is the
line that makes the list usable on Monday rather than interesting on Friday.

---

## One row, fully expanded

This is row 1 with every field the system filled, and the basis for each.

```
company              Northline Mechanical
domain               northlinemech.example
hq_location          Fort Wayne, IN
country              US
sector               Commercial building services
segment              Commercial contract-recurring HVAC service

ownership_type       founder-owned
ownership_evidence   Tier 1 — Indiana SOS filings list the same sole officer
                     since 1994 incorporation; no share transfers on record.
                     Cross-checked against company about page dated 2026-02.
evidence_tier        1
sponsor_screen       clear — screened against the 5 sponsor platforms named in
                     the market map, no trade press, no UCC filings naming a
                     fund entity

year_founded         1994
employee_count       142   (LinkedIn 2026-09, cross-checked against 138 stated
                     in a 2026-06 trade press piece)

est_revenue          $18-23M
                     (estimate: 142 staff x $130-165k sector-typical revenue
                     per head from the MCAA 2025 regional benchmark;
                     headcount firm, two independent sources. Cross-check:
                     $16.1M floor implied by disclosed 2024-25 state and
                     municipal contract awards.)
est_ebitda           $2.9-4.1M
                     (estimate: 16-18% sector-typical margin from map segment
                     economics applied to the revenue range; both ranges
                     unverified)
financial_confidence high   (two methods agree within 15%)

fit_role             platform
fit_role_reason      Top half of the size box; named GM and named service
                     manager, neither a family member; contract maintenance
                     base stated at 55% of revenue in the 2026-06 piece; no
                     existing platform within 150 miles

verdict              PRIORITY
fit_reason           Clean on all exclusions; founder-owned at Tier 1;
                     estimate midpoint inside size box; platform role decided
                     with second-tier management evidenced; all 4 must-haves
                     met; high-strength leadership signal 4 months old
excluded_by          N/A

signal               "I'm 63. My daughter's a physician and my son has no
                     interest in the trade. At some point this business needs
                     an owner who isn't me."
signal_family        leadership
signal_source        https://example-tradepress.test/northline-mechanical-30
evidence_date        2026-06-14
signal_strength      high   (Tier 2, the owner on the record, 4 months old,
                     about a decision rather than an atmosphere)

source               Indiana mechanical contractor licence roster (complete
                     pull, 2026-10-02); cross-found in MCAA member directory
                     and 2025 + 2026 AHR exhibitor lists
date_added           2026-10-07
status               ranked

NOT KNOWN            Margin is a sector benchmark, not theirs. No accounts
                     filed. Customer concentration unknown. Whether the GM
                     would stay post-transaction is unknown and material to
                     the platform case.
```

The `NOT KNOWN` block is on every PRIORITY row. It is the difference between a
brief and a sales pitch to yourself.

---

## Why rows did not make PRIORITY

```
WATCH — 79 rows

  fits, no signal found                     41
  fits, signal below the recency window      9
  fits, signal strength low                  8
  ownership Not found                       11
  revenue Not found, nothing contradicts     6
  edge of the size box on an estimate        3
  role neither clean platform nor add-on     1

PASS — 105 rows

  ownership    38   ← 23 sponsor-owned (9 of these market themselves as
                      family owned), 11 corporate subsidiaries out of scope,
                      4 publicly listed
  strategic    31   ← 19 out-of-scope segment, 7 portfolio conflict,
                      5 already worked and closed out
  economics    24   ← verified figures only. 16 below the revenue floor on
                      filed accounts, 8 above the ceiling
  geography    12
```

The nine sponsor-owned companies still presenting themselves as family owned are
the single most valuable line in this report. Each one is a letter that does not
get written to an owner who sold two years ago.

---

## The audit

Runs every time, reported whether or not it is clean.

```
AUDIT — 2026-10-09

1. PRIORITY signals verified at source        10 of 14 checked
     quote confirmed at URL                    9
     quote not found on page                   1  ← Mansell Mechanical.
                                                  Page rewritten since
                                                  capture. Signal downgraded
                                                  to Not found, row moved to
                                                  WATCH. PRIORITY now 13.

2. False negatives among PASS rows            20 random rows pulled
     look correctly excluded                  18
     worth a second look                       2  ← Barrow Air Systems
                                                  (excluded on a $7.4M
                                                  revenue estimate, floor is
                                                  $8M, estimate was low
                                                  confidence — rule 7 says
                                                  this should have been
                                                  WATCH. Corrected.)
                                                  Dalemount Services
                                                  (excluded on geography,
                                                  HQ is 148 miles from
                                                  Columbus, inside the add-on
                                                  radius. Corrected.)

3. Keep pile re-screened                      93 rows
     new sponsor hits                          1  ← Vennor Mechanical,
                                                  acquired 2026-09, announced
                                                  after our capture. Moved to
                                                  PASS.
     new exclusion hits                        0

4. Distribution                               inside band

Net after audit: PRIORITY 13, WATCH 82, PASS 103.
Three corrections, all in the direction the rubric requires.
```

An audit that catches nothing on a 200-row list has usually not run properly.

---

## What you actually do with it

Thirteen rows, each with a named role, a sourced reason to call this quarter, and
an honest list of what is still unknown. That is a fortnight of associate time
compressed, and it is the point where this package stops and you take over.

Finding the owner's contact details, writing the approach and tracking the
replies are deliberately not in here. Different job, different rules, and doing
it badly is worse than not doing it.
