# Buy Box Mapper

Type a buy box. Get back a ranked list of off-market companies that fit it.

Six skills, three agents and one command that take an acquisition mandate and
return a prioritised target list — sector, geography, revenue, estimated EBITDA,
ownership, platform or add-on fit, and a dated reason to call this quarter — with
the rule that produced every verdict written next to it.

No associate reading two hundred companies one at a time.

Built for PE funds, family offices, search funds, independent sponsors, holdcos
and corporate development teams.

Runs on [Claude Code](https://www.anthropic.com/claude-code) and local files.
No database, no API keys, no signups.

---

## 👉 Start here: [SETUP.md](./SETUP.md)

Fifteen minutes from zero to a ranked list. Every step in plain English.

Want to see the end product first?
**[samples/sample-output.md](./samples/sample-output.md)** is a complete finished
run, invented end to end, so you know exactly what you are getting before you
install anything.

---

## Came from the LinkedIn post? — this is the system

### One command

Fill in one file, then type:

```
/map-buy-box
```

The run stops and shows you its work before every write. Five steps, five
approval gates, nothing happens behind your back.

### Every row comes back with this

| Field | What it holds |
|---|---|
| company, domain, HQ | identity and geography |
| sector, segment | where it sits in the map |
| ownership_type | founder, family, management, ESOP, sponsor, corporate, or `Not found` |
| ownership_evidence | the filing or register that establishes it, with a tier and a date |
| sponsor_screen | the check that catches companies already bought but still marketing themselves as family owned |
| est_revenue, est_ebitda | a range, labeled an estimate, with the basis attached |
| financial_confidence | verified / high / medium / low / `Not found` |
| fit_role | `platform` or `add-on`, and for an add-on, the named platform it attaches to |
| signal | the reason to call this quarter, quoted verbatim, with a working URL and a date |
| signal_strength | high / medium / low / `Not found` |
| verdict | **PRIORITY** / **WATCH** / **PASS** |
| fit_reason | the rules that fired, so a verdict can be argued with in March |

Three verdicts, not a score out of 100. A number between 1 and 100 invites an
argument about whether a 71 beats a 68 and tells nobody what to do on Monday.

**PRIORITY** — strong mandate fit, strong reason to engage now
**WATCH** — fits the thesis, needs a better trigger
**PASS** — wrong ownership, economics, geography, or strategic fit

### The six skills

| Skill | What it does |
|---|---|
| `buy-box-intake` | Checks the box is complete enough to map against, rewrites untestable must-haves into tests, scopes the run. Runs a principal-buyer gate that has no override |
| `buy-box-market-map` | Maps the segment the box implies: fragmentation, who is already consolidating, the typical owner, the segment economics every later estimate depends on, and where these companies are actually findable. Ends with a verdict that is sometimes "do not source this segment" |
| `buy-box-discovery` | Enumerates the population from licence rosters, registries, association directories, exhibitor lists and dealer locators — the sources bought lists never cover — with a source per row and a coverage log that names what the pull missed |
| `buy-box-ownership-and-size` | Who actually owns it, the sponsor screen, a defensible size read on companies that publish nothing, and the platform or add-on call |
| `buy-box-signals` | The four families — growth, hiring, financing, leadership — quoted verbatim, sourced, dated, and aged against a per-family recency window |
| `buy-box-ranking` | Builds a rubric from your box, gets it approved before ranking a single row, ranks every row identically, then audits itself |

Install, then run `/skills` to see all six.

### The three agents

| Agent | What it does |
|---|---|
| `buy-box-mapper` | Box, map, population. Stops at the list of company names |
| `buy-box-analyst` | Ownership, size, role, signals. Fills in what the ranking needs to know |
| `buy-box-ranker` | Rubric, ranking, audit. Turns research into decisions |

Install, then run `/agents` to see all three.

> Both lists are the same system. The agents run the skills.

### The chain

```
buy-box-intake                  box checked, run scoped
      ↓
buy-box-market-map              segment economics, sources, verdict
      ↓
buy-box-discovery               population enumerated, deduped, sourced
      ↓
buy-box-ownership-and-size      owner, sponsor screen, revenue, EBITDA, role
      ↓
buy-box-signals                 the dated reason to call this quarter
      ↓
buy-box-ranking                 PRIORITY / WATCH / PASS, then the audit
```

---

## The rules that make the list trustworthy

Any system can return two hundred ranked rows. These are the rules that decide
whether the ranking means anything.

- **Unknown is not failed.** `Not found` revenue is not a failed size test.
  Ranking gaps as negatives systematically deletes the least-marketed companies
  from the list, which is to say the proprietary ones
- **Estimates are labeled, and the label travels with the number.** A labeled
  estimate outside your size box makes a row WATCH, never PASS. Only a verified
  figure excludes on economics
- **Sponsor-owned is always PASS.** The screen runs on every row, including the
  ones that look obviously founder-owned, because companies keep the family-owned
  language for years after a sale
- **A thin website is not a negative signal.** The companies with no marketing
  budget are the ones no banker has called
- **Fit and timing stay separate.** A loud signal never promotes an out-of-mandate
  company. A missing signal never deletes an in-mandate one
- **Signals are quoted verbatim or they do not exist.** "We are exploring options
  for the next phase" is a quote. "The founder is looking to sell" is a
  fabrication, and it is the kind that ends up in an email to the founder
- **The audit runs every time and gets reported whether or not it is clean**
- **Nothing is deleted.** A PASS carries the rule that excluded it, so the same
  company is not rediscovered and re-researched in six months

---

## What this deliberately does not do

No contact finding. No outreach drafting. No pipeline tracking. No sending.

The package stops at the ranked list, which is the part that costs a fortnight of
associate time. Finding the owner, writing the approach and handling the replies
are a different job with different rules, and doing them badly is worse than not
doing them.

---

## Repo contents

- [`SETUP.md`](./SETUP.md) — the full setup guide, start here
- [`commands/`](./commands/) — the `/map-buy-box` command
- [`skills/`](./skills/) — the six skills Claude Code reads
- [`agents/`](./agents/) — the three subagents
- [`references/`](./references/) — the ranking rubric, estimation rules, signal
  evidence rules, and where the companies actually are
- [`templates/`](./templates/) — the buy box template, a fully worked example
  buy box, and the 29-column `targets.csv`
- [`samples/`](./samples/) — a complete finished run, so you can see the output
  before you install

---

## A word on the research

Everything here runs on public sources: registers, licence rosters, filings,
procurement awards, trade press, association directories, and what companies
publish about themselves.

Nothing in this package scrapes behind a login, pretends to be somebody it is
not, or guesses an email address. If you are a fee-based intermediary rather than
a principal buyer, the intake skill will stop and tell you to talk to securities
counsel before it researches anybody on your behalf. That gate is deliberate and
has no override.

---

Free and MIT licensed. Built by [Corebits](https://corebits.io).
