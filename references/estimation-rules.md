# Estimation Rules — Revenue and EBITDA on Companies That Publish Nothing

Private companies do not publish numbers. You still need a size read, because
"inside the size box" is a gate in the ranking rubric and a blank cannot pass
through a gate.

So the rule here is not "find the number". It is **produce a range, attach the
basis, label it an estimate, and never let the label fall off.**

---

## Verified versus estimated

**Verified** means the company or a filing published it:

- Companies House full or abridged accounts (UK) and equivalent statutory
  filings elsewhere
- A public contract award value
- A figure the company stated publicly, on the record, with a date
- A regulatory filing disclosing revenue

Everything else is an estimate. **An M&A database revenue field is an estimate
somebody else made**, usually by the first method below. Treat it as one data
point, name it as the source, and never let repetition turn it into
verification.

---

## The five methods

Use at least two. Report the spread, not a point.

**1. Revenue per head.** Headcount multiplied by a sector-typical range taken
from the market map. State where the headcount came from and how firm it is.
This is the workhorse method and also the weakest one, because it inherits every
error in the headcount.

**2. Public comparables.** A listed or recently sold company in the same segment
at similar scale. Name it. Adjust for the obvious differences.

**3. Capacity.** Trucks, chairs, beds, routes, machines, licensed seats, square
footage, rigs, bays — whatever the segment actually runs on. Often the best
method in services, logistics and healthcare, and usually the most defensible.

**4. Contract and award records.** Public awards and framework agreements give
you a floor. A floor is honest and useful, and it is a verified floor rather
than an estimated midpoint.

**5. Trade or association data.** Membership tiers, published sector averages,
regional benchmarks. Weak alone, good as a cross-check.

Where two methods disagree by more than about 40 percent, say so, widen the
range, and drop the confidence rating. Do not pick the one you prefer.

---

## Write it with the label attached

Never this:

```
est_revenue: $12M
```

Always this:

```
est_revenue: $10-14M (estimate: 85 staff x $130-165k sector-typical revenue
             per head from OSHMA 2025 benchmark; headcount from LinkedIn
             2026-05, unverified. Cross-check: $11.2M implied by 2024 state
             contract awards as a floor.)
```

**The label travels with the number.** A stripped estimate becomes a fact the
moment somebody pastes it into a second document, and a confident wrong revenue
figure in a first conversation with an owner is not recoverable.

### EBITDA

Only ever a margin band applied to a revenue range:

```
est_ebitda: $1.5-2.5M (estimate: 15-18% sector-typical margin from map
            segment economics, applied to the $10-14M revenue estimate;
            both ranges unverified)
```

Never a point estimate. Never a margin you cannot source. An EBITDA estimate
built on a revenue estimate is two estimates stacked, and the range has to show
it.

---

## Confidence ladder

| Confidence | Test |
|---|---|
| **verified** | A filing or the company published it |
| **high** | Two independent methods agree within about 25 percent |
| **medium** | One good method, or two with a wider spread |
| **low** | One weak method, or a headcount that is itself a guess |
| `Not found` | No defensible method available |

Write it to `financial_confidence`. A range with no confidence rating is a range
nobody downstream can weigh.

---

## What an estimate is allowed to do to a ranking

This is the part that matters, and it is deliberately asymmetric.

- A **verified** figure outside the size box is a **PASS** on economics
- A **labeled estimate** outside the size box is a **WATCH**, never a PASS
- `Not found` revenue is **not a failed size test**. The row ranks on everything
  else and lands at WATCH

Excluding a real target because a headcount guess landed 15 percent under the
floor is the most expensive routine error in origination, and it happens
silently. The asymmetry is the fix.

---

## Hard rules

**1. Two methods minimum, or the confidence is `low`.**

**2. The basis string is not optional.** No basis, no number.

**3. Never estimate a valuation or a multiple.** Different discipline, and a
wrong number there is worse than no number.

**4. Never carry an estimate into an outreach draft.** Owners know their own
revenue. An estimate is an internal ranking input and nothing else.

**5. Name the benchmark every time.** One sourced sector figure usually
underpins the entire list. The report should make that dependency visible rather
than hiding it inside two hundred rows.

**6. If the market map has no revenue per head and no typical margin, stop.**
Every estimate depends on a sourced sector benchmark. Inventing one propagates a
made-up number into every row on the list, and they will all be wrong the same
way, which is the hardest kind of wrong to notice.
