# Ranking Rules — PRIORITY / WATCH / PASS

The whole point of this package is that nobody has to read two hundred companies
one at a time to find the nine worth a call. That only works if the ranking is
mechanical: the same rules applied to every row, in the same order, with the rule
that fired written next to the answer.

Three buckets. Not five, not a score out of 100. A number between 1 and 100
invites an argument about whether a 71 beats a 68 and tells nobody what to do on
Monday. These three tell you exactly what to do.

---

## The two dimensions, kept separate

Every row gets ranked on two questions that must never be allowed to contaminate
each other.

**Fit** — does this company belong in the mandate at all? Sector, geography,
size, ownership, platform or add-on role, must-haves, exclusions.

**Timing** — is there a sourced, dated reason to call this quarter rather than
some other quarter?

A company can have perfect fit and no timing. That is a WATCH, and it is a
valuable row. A company can have a loud timing signal and sit outside the
mandate. That is a PASS, and the signal does not rescue it.

Collapsing the two is the most common way a ranked list ends up flattering
whoever built it.

---

## The three buckets

### PRIORITY — strong mandate fit, strong reason to engage now

All six must be true:

1. Clean on every hard exclusion in the buy box
2. `ownership_type` is actionable **and is not `Not found`**
3. Inside the size box on verified figures, or on a labeled estimate whose
   midpoint sits inside the box
4. `fit_role` is decided — `platform` or `add-on` — with a reason
5. Meets every must-have in the buy box
6. Carries a sourced, dated, quotable timing signal at `signal_strength` = high
   or medium

### WATCH — fits the thesis, needs a better trigger

The mandate fit is real. The reason to call is not there yet, or the file is too
thin to know.

Typical WATCH rows:

- Fits everything, no signal found
- Fits everything, signal found but `signal_strength` = low
- Fits everything, signal found but older than the recency window
- Ownership is `Not found` and everything else is clean
- Revenue is `Not found` and nothing contradicts the size box
- Inside the thesis but at the edge of the size box on an estimate
- Fits as neither a clean platform nor a clean add-on and needs a human view

**WATCH is a keep, not a soft reject.** Mandates widen, companies grow, and
owners change their minds on a schedule nobody publishes. Re-ranking a WATCH row
next quarter costs nothing. Losing it costs a deal.

### PASS — wrong ownership, economics, geography, or strategic fit

Those four reasons, and only those four, produce a PASS. Record which one in
`excluded_by`.

- **Ownership** — sponsor-owned platform or add-on, public, or an ownership type
  the buy box puts out of scope
- **Economics** — verified revenue or EBITDA outside the box, or a business model
  the thesis excludes
- **Geography** — outside a stated geographic constraint
- **Strategic** — out-of-scope segment, a portfolio conflict, a named
  competitor, or a company already worked and closed out

A PASS is a decision, not a deletion. Rows stay on the list carrying the rule
that excluded them, so the same company does not get rediscovered and
re-researched in six months.

---

## The order the rules run in

Always this order. It is not cosmetic: running size before ownership wastes
estimation work on companies a sponsor already owns.

1. Hard exclusions
2. Ownership gate
3. Geography gate
4. Segment and business model gate
5. Size box
6. Platform or add-on role
7. Must-haves
8. Timing signal
9. Bucket
10. `fit_reason` string naming the rules that fired

---

## The hard rules

Not tunable per mandate. Each one exists because breaking it produces a specific
and expensive failure.

**1. No bucket without a `fit_reason` naming the rules applied.**
A bucket without a reason is a guess wearing a label.

**2. Sponsor-owned is always PASS.** Platform or add-on, whatever the fit looks
like otherwise. Record `excluded_by` = ownership. The sponsor screen is the most
commonly missed step in origination and the most embarrassing one to miss out
loud, in writing, to an owner who sold two years ago.

**3. Unknown is not failed.** `Not found` revenue is not a failed size test.
`Not found` ownership is not a failed ownership test. Rank a gap as a gap.
Ranking gaps as negatives systematically deletes the least-marketed companies
from the list, which is to say the proprietary ones.

**4. `Not found` ownership can never be PRIORITY.** Whatever else is true. You
cannot call an owner you have not identified.

**5. A thin website is not a negative signal.** Rank on registry facts, licences,
tenure, headcount, reviews, hiring, certifications and filings. Never on design
quality. Broken, this rule inverts the result in exactly the market you are
trying to reach: the companies with no marketing budget are the ones no banker
has called.

**6. Fit and timing stay separate.** A strong signal never drags an
out-of-mandate company up. A missing signal never pushes an in-mandate company to
PASS. That is what WATCH is for.

**7. Estimates are labeled, and a labeled estimate never produces a PASS on its
own.** An estimate outside the box makes a row WATCH, not PASS. Only a verified
figure excludes on economics.

**8. When genuinely torn between PRIORITY and WATCH, choose WATCH. When torn
between WATCH and PASS, choose WATCH.** The expensive error in origination is
deleting a real target on thin information. The cheap error is carrying one extra
row.

**9. Never move a row to make the distribution look better.**

**10. Any rubric change re-ranks the whole list.** A list ranked under two
rubrics is two lists interleaved and nobody downstream can tell which is which.

---

## Platform or add-on

The buy box decides what each role requires. The rubric only enforces that the
question gets answered rather than left blank.

| Role | Usually requires |
|---|---|
| `platform` | Management that can run without the seller, systems that survive a transition, the top of the size box, a defensible position in its segment |
| `add-on` | Geographic or capability adjacency to a named existing platform, the bottom of the size box, customer overlap that is complementary rather than duplicated |
| `either` | Genuinely could go both ways. Allowed, but say which existing platform the add-on case would attach to |
| `Not found` | Not enough known yet. Caps the row at WATCH |

Write the adjacency explicitly for an add-on. "Add-on to the Ohio platform,
extends coverage into western Pennsylvania where that platform currently
subcontracts" is a usable answer. "Add-on" on its own is not.

---

## Healthy distributions

For a properly scoped mandate against a genuinely mapped market:

| Bucket | Healthy | What it means outside that range |
|---|---|---|
| PRIORITY | 5-15% | Above 25%: the rubric is flattering the user, or signals are being read generously. Below 3%: discovery is off-thesis, or the signal pass has not run yet |
| WATCH | 30-50% | Below 20%: the rubric is ranking gaps as failures. Check hard rule 3 |
| PASS | 30-50% | Above 70%: discovery is pulling the wrong population. Fix discovery, not the rubric |

If fewer than 5 percent of rows survive, stop. Either discovery is aimed at the
wrong market or the buy box is narrower than the market can support. Both are
worth knowing before a week of research goes into it.

---

## The audit

Runs every time, including when the numbers look fine. Four parts.

1. **Verify 10 PRIORITY signals at source.** Open the `signal_source` URL and
   confirm the quoted words actually appear there. Report every one that does
   not. This is the single most important thing the audit does: it is the check
   that catches a fabricated quote before it reaches an owner
2. **Pull 20 random PASS rows and hunt for false negatives.** If any look
   obviously good, the filter is too tight. Report them by name
3. **Re-screen the keep pile against sponsors and the exclusion list.** Anything
   that hits was missed upstream
4. **Sanity check the distribution** against the table above

Report the audit whether or not it is clean. An audit that is never reported is
an audit that never ran.
