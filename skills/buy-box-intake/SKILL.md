---
name: buy-box-intake
description: "Read a buy box, check it is complete enough to map against, run the principal-buyer gate, and scope the run before any research starts. Turns a vague mandate into testable criteria and refuses to proceed on a box that would produce a confidently wrong list. Triggers on: help me fill out my buy box, check my buy box, is my buy box ready, start a mapping run, set up the run, map my buy box, I want to find companies that fit this."
---

# Buy Box Intake

Every bad target list starts the same way: somebody mapped a mandate that had
never been written down properly. The list comes back plausible, nobody can say
which rows are wrong, and the whole run has to be repeated.

This skill is the gate. It is short, it is strict, and it runs before anything
else in the package.

**Read first:**
- `references/ranking-rubric.md` — what the box has to be able to answer
- `templates/BUY-BOX.md` — the structure
- `templates/BUY-BOX-example.md` — what a usable one looks like

---

## Step 1 — Find or create the box

Look for `BUY-BOX.md` or `buy-box.md` in the working folder.

If there is none, offer to fill one out conversationally, section by section, and
write it. Do not research anything first. A box filled in after a market map is
a box the map has already biased.

---

## Step 2 — The principal-buyer gate

Read section 1. This runs before any other check and it has no override.

**If the user is buying as a principal** — their own capital, committed capital,
or a fund — continue.

**If the user earns a fee for introducing or arranging a transaction they do not
buy**, stop and say this:

> You have described a fee-based intermediary role. In the US, researching
> private companies and approaching owners about selling, for a fee, can require
> broker-dealer registration, and the rules differ by state and by how the fee is
> structured. There is a limited M&A broker exemption and it is narrower than
> most people assume.
>
> I am not able to give you legal advice and I am not going to research a target
> list for you on this basis. Talk to securities counsel first. If you are
> buying as a principal, correct section 1 and we can start.

Do not soften it, do not offer a partial run, and do not proceed because the user
says it is fine. If they change section 1, ask them to confirm they have actually
changed their role and not just the file.

**Outside the US**, flag that equivalent rules exist in most jurisdictions and
the same conversation with counsel applies.

---

## Step 3 — Completeness check

Nine things have to be answerable. Report the state of each.

| # | Must be answerable | Where | If missing |
|---|---|---|---|
| 1 | Principal buyer or not | §1 | **Hard stop** |
| 2 | Size box, revenue floor and ceiling | §3 | **Hard stop** — there is no size gate without it |
| 3 | At least one sector and one segment | §4 | **Hard stop** — nothing to enumerate |
| 4 | Geography | §5 | **Hard stop** — the gate that removes most rows |
| 5 | Which ownership types are in scope | §7 | **Hard stop** — ownership gates everything |
| 6 | Between 2 and 6 must-haves | §6 | Ask. Zero means nothing is tested. Twelve means nothing survives |
| 7 | Named existing platforms, if add-ons are wanted | §2 | Ask. Without them, no add-on verdict has a test behind it |
| 8 | Portfolio companies and named competitors | §8 | Ask. This is the conflict screen |
| 9 | Run size and what would make the run worth it | §10 | Ask. Default 150 companies if they have no view |

`TBD` is an acceptable answer on 6 to 9 and the run can start. `TBD` on 1 to 5
cannot.

---

## Step 4 — Challenge the box

This is the part that earns its keep. Say these out loud where they apply.

- **Must-haves that are not testable.** "Strong management team" is not a test.
  "A named second-tier manager who is not the owner and not the owner's child"
  is. Rewrite each one into something a researcher could verify or fail
- **A size box narrower than the market.** $20-25M revenue in a segment where
  the typical operator does $4M will return almost nothing. Say so now, not
  after the run
- **Must-haves that contradict the ownership scope.** Requiring audited accounts
  while targeting founder-owned companies under $15M removes most of the
  population
- **Add-ons with no platform named.** Go back to section 2
- **An exclusion list that excludes the thesis.** It happens. Read 4 and 8
  against each other
- **A geography that is a country when the thesis is local.** "US" plus "within
  150 miles of a platform" are different mandates, and only one of them is
  mappable

Propose specific rewrites. Do not just flag problems.

---

## Step 5 — Scope the run

Write the run plan and get it approved before anything else starts.

```
RUN PLAN

Mandate      [one line from §2]
Segments     [from §4, the ones this run covers]
Geography    [from §5]
Size box     [from §3]
Ownership    [in-scope types from §7]
Must-haves   [the rewritten, testable list]

Target population    ~150 companies
Expected PRIORITY    8-22 rows (5-15% of ranked)

Sequence
  1. buy-box-market-map          [segment economics, where to look, verdict]
  2. buy-box-discovery           [enumerate, dedupe, source per row]
  3. buy-box-ownership-and-size  [ownership, sponsor screen, revenue, EBITDA]
  4. buy-box-signals             [the four families, quoted and dated]
  5. buy-box-ranking             [rubric, rank, audit]

Each step stops and shows you its output before writing.
```

### 🚧 HARD GATE

Show the run plan, every challenge from step 4, and every `TBD`. Get approval.
Then write `BUY-BOX.md` if you changed it, and `targets.csv` from the template
with the example row removed.

---

## Step 6 — Report

```
INTAKE COMPLETE

Principal buyer gate     passed
Completeness             5 of 5 hard requirements answerable
                         §7 platforms named (2), §10 run size set (150)
Rewritten must-haves     3 of 4 made testable, shown above and approved
Flagged                  size box floor sits below the segment's typical
                         operator — expect a wide WATCH band at the bottom

Workspace
  BUY-BOX.md             updated
  targets.csv            created, empty, 29 columns

Next: buy-box-market-map. Nothing has been researched yet.
```

---

## Notes

- **Never research during intake.** Not one search. The box has to describe what
  the user wants, not what the first page of results suggests is available
- **Do not fill a gap with a sensible default.** A sensible default in a buy box
  becomes an unexamined criterion that excludes real companies silently. `TBD`
  and a question beats a default every time
- **Sections 4 and 9 will improve after the market map.** Say so, and schedule
  the revisit rather than pretending the box is final
- **The principal-buyer gate is not a formality.** It is the one rule in this
  package that exists to protect the user from themselves
