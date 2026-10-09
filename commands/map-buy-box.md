---
description: Map a buy box to a ranked list of off-market companies — the full five-step run, with an approval gate before each write
argument-hint: "[optional: a segment or geography to scope this run]"
---

# Map the buy box

Run the full mapping chain for the buy box in this folder. Scope for this run, if
the user gave one: `$ARGUMENTS`

You are driving five skills in order. Each one stops and shows its output before
it writes anything. Do not skip a gate, do not batch the gates together at the
end, and do not continue past a step the user has not approved.

## Before you start

Read, in this order:

1. `BUY-BOX.md` in this folder. If it does not exist, say so and offer to fill
   one out section by section from `templates/BUY-BOX.md`. Do not research
   anything first
2. `references/ranking-rubric.md`
3. `references/estimation-rules.md`
4. `references/signal-evidence-rules.md`
5. `references/sourcing-directories.md`

The `references/` files live in the cloned repo, not in this folder. If you
cannot find them, ask the user for the path to their clone rather than proceeding
without them.

## The run

**1. `buy-box-intake`**
Check the box, run the principal-buyer gate, challenge the untestable
must-haves, write the run plan.
→ Gate: the run plan and every challenge. Stop for approval.

**2. `buy-box-market-map`**
Segment definition, population and fragmentation, segment economics, the typical
owner, who is already consolidating, where the companies are findable, verdict.
→ Gate: the map and the verdict. Stop for approval.
→ If the verdict is DO NOT SOURCE IT, stop the run there and say why.

**3. `buy-box-discovery`**
Enumerate from the sources the map named. Cross-find, dedupe, apply only the
geography and segment gates, write the coverage log.
→ Gate: counts by source, the coverage log, 15 sample rows. Stop for approval.

**4. `buy-box-ownership-and-size`** then **`buy-box-signals`**
Ownership and the sponsor screen, then labeled revenue and EBITDA ranges, then
the platform or add-on role, then the four signal families.
→ Gate after each, in batches of 20 to 30 rows. Stop for approval.

**5. `buy-box-ranking`**
Build the rubric, get it approved before ranking a single row, rank in the fixed
order, run the four-part audit, save the rubric.
→ Gate: the rubric before ranking. Then the ranked list with the audit.

## What you hand over at the end

- `targets.csv` — every row ranked, with the rule that ranked it
- The PRIORITY rows summarised in chat, each with its role, its signal and its
  `NOT KNOWN` block
- `market-map-[segment]-[date].md`
- `rubric-[segment]-[date].md`
- The audit in full, including every correction it produced

## Rules that hold across the whole run

- **Never fabricate.** No invented domains, headcounts, quotes, URLs or revenue
  figures. `Not found` is a real answer and the most common one
- **Every estimate carries its basis.** The label travels with the number
- **Unknown is not failed.** A gap ranks as a gap, never as a negative
- **Sponsor-owned is always PASS**
- **Fit and timing stay separate**
- **Public sources only**
- **Rows are never deleted**, only ranked

## Where this stops

At the ranked list. Finding owner contact details, writing the approach and
tracking replies are not in this package. When the user asks for the next step,
say that plainly rather than improvising it.
