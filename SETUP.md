# Buy Box Mapper — Setup Guide

> A free giveaway. Six skills, three agents and one command that take an
> acquisition buy box and return a ranked list of off-market companies: sector,
> geography, revenue, estimated EBITDA, ownership, platform or add-on fit, and a
> dated reason to call this quarter.
>
> Follow this guide end to end and you will have it running on your own machine
> in about fifteen minutes. No database, no API keys, no signups.

---

## What this actually is

**One command.** You fill in one file and type `/map-buy-box`. The run goes
through five steps and stops for your approval before each write.

**The six skills** are what actually runs. You can call any of them directly.

| Skill | What it does |
|---|---|
| `buy-box-intake` | Checks your box is complete enough to map against, rewrites untestable must-haves into tests, scopes the run |
| `buy-box-market-map` | Maps the segment your box implies: fragmentation, who is consolidating, the typical owner, the segment economics every estimate depends on, where these companies are findable. Ends with a verdict |
| `buy-box-discovery` | Enumerates the population from licence rosters, registries, association directories and exhibitor lists, with a source per row |
| `buy-box-ownership-and-size` | Who owns it, the sponsor screen, labeled revenue and EBITDA ranges, and the platform or add-on call |
| `buy-box-signals` | Growth, hiring, financing and leadership signals — quoted, sourced, dated, aged |
| `buy-box-ranking` | Builds a rubric from your box, gets it approved, ranks every row identically, audits itself |

**The three agents** are the team. You talk to them like people.

| Agent | What it does |
|---|---|
| `buy-box-mapper` | Box, map, population |
| `buy-box-analyst` | Ownership, size, role, signals |
| `buy-box-ranker` | Rubric, ranking, audit |

Everything runs through conversation. Your data stays in local files on your
machine.

**Want to see the output first?** Read
[`samples/sample-output.md`](./samples/sample-output.md). It is a complete
finished run, invented end to end, and it will take you three minutes.

---

## What you need

| Thing | Cost | Required? |
|---|---|---|
| [Claude Code](https://www.anthropic.com/claude-code) | Claude subscription or API usage | **Yes** |
| A folder on your computer | Free | **Yes** |
| A written buy box | Free, and ten minutes | **Yes** |
| Everything else | — | No |

That is the whole list. There is deliberately no database, no MCP server and no
API key to configure.

---

# Part 1 — Install Claude Code

Claude Code is Anthropic's official terminal app for Claude. It runs everything
here.

Follow the official instructions at
**[anthropic.com/claude-code](https://www.anthropic.com/claude-code)**. macOS,
Windows and Linux are all supported.

Then check it works:

```bash
claude
```

You should get a welcome screen and a prompt. Type `/login` and authenticate if
you have not already. Exit with Ctrl+C twice.

---

# Part 2 — Install the package

Two steps: clone the repo, then copy the pieces where Claude Code looks for them.

### macOS / Linux

```bash
git clone https://github.com/corebits-io/buy-box-mapper.git
mkdir -p ~/.claude/skills ~/.claude/agents ~/.claude/commands
cp -r buy-box-mapper/skills/* ~/.claude/skills/
cp -r buy-box-mapper/agents/* ~/.claude/agents/
cp -r buy-box-mapper/commands/* ~/.claude/commands/
```

### Windows (PowerShell)

```powershell
git clone https://github.com/corebits-io/buy-box-mapper.git
New-Item -ItemType Directory -Force "$HOME\.claude\skills", "$HOME\.claude\agents", "$HOME\.claude\commands"
Copy-Item -Recurse -Force "buy-box-mapper\skills\*" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force "buy-box-mapper\agents\*" "$HOME\.claude\agents\"
Copy-Item -Recurse -Force "buy-box-mapper\commands\*" "$HOME\.claude\commands\"
```

### Keep the cloned folder

Do not delete it. The skills read the `references/` files from it, and you will
copy the `templates/` in a moment.

### Verify

Start Claude Code and run:

```
/skills
```

You should see all six: `buy-box-intake`, `buy-box-market-map`,
`buy-box-discovery`, `buy-box-ownership-and-size`, `buy-box-signals`,
`buy-box-ranking`.

Then:

```
/agents
```

You should see `buy-box-mapper`, `buy-box-analyst`, `buy-box-ranker`.

If either list is short, see Troubleshooting below.

---

# Part 3 — Set up your workspace

This is where your actual data lives. Keep it separate from the cloned repo.

```bash
mkdir -p ~/my-mapping
cd ~/my-mapping
cp ~/buy-box-mapper/templates/BUY-BOX.md .
cp ~/buy-box-mapper/templates/targets.csv .
```

Windows:

```powershell
New-Item -ItemType Directory -Force "$HOME\my-mapping"
Set-Location "$HOME\my-mapping"
Copy-Item "$HOME\buy-box-mapper\templates\BUY-BOX.md" .
Copy-Item "$HOME\buy-box-mapper\templates\targets.csv" .
```

> **Never put this folder in a public repository.** It will contain company
> names, owner names and the reasoning behind a live acquisition thesis. Owner
> names are personal data and are regulated in most jurisdictions.

Delete the example row from `targets.csv` before you start. It is there to show
you what a correctly filled row looks like.

---

# Part 4 — Fill out your buy box

**This is the most important step in the whole guide.** Do not skip it and do not
rush it.

`BUY-BOX.md` is the file every skill reads. It is where the system learns what you
buy, what size, where, which ownership types are actionable, what you will never
touch, which platforms an add-on could attach to, and which timing signals matter
most for your thesis.

Open it and fill it out honestly. Ten minutes here decides whether the ranked
list is useful or plausible-looking rubbish.

**Three rules while filling it in:**

1. If something does not apply, write `N/A`
2. If you do not know yet, write `TBD`. The system will ask rather than invent
3. **Answer section 1 properly.** If you are a fee-based intermediary rather than
   a principal buyer, the intake skill will stop and tell you to talk to counsel
   about broker-dealer registration before researching anybody. That gate is
   deliberate and has no override

**Two sections people skip, and should not:**

- **Section 2, the named platforms.** If you want add-ons, name the existing
  platforms they would attach to. Without them, "add-on" is a label with no test
  behind it, and every add-on verdict on your list will be a guess
- **Section 6, the must-haves.** Three to five real requirements beats twelve
  aspirations. And make them testable: "strong management team" is not a test,
  "a named second-tier manager who is not the owner and not the owner's child"
  is. The intake skill will push back on the ones that are not, but it is faster
  if you do it first

**Stuck?** Read [`templates/BUY-BOX-example.md`](./templates/BUY-BOX-example.md).
It is a complete worked box for a fictional fund, and it is the fastest way to
see the level of specificity that works.

Or do it conversationally. Start Claude Code in the folder and say:

```
help me fill out my buy box
```

Sections 4 and 9 will improve after your first market map. That is expected. Come
back and update them.

---

# Part 5 — Your first run

Start Claude Code from your workspace folder:

```bash
cd ~/my-mapping
claude
```

Then:

```
/map-buy-box
```

That runs the whole chain. Here is what happens at each gate, so you know what
you are approving.

### 1. Intake

It reads your box, runs the principal-buyer gate, and challenges anything that
cannot be tested. Expect it to rewrite a must-have or two and to tell you if your
size box looks narrower than the market can support.

**You approve:** the run plan.

### 2. Market map

It maps the segment your box implies before enumerating a single company.
Fragmentation, the typical owner, who is already consolidating, and — the part
that matters most — the segment economics: revenue per head and typical EBITDA
margin, sourced and dated. Every revenue estimate later in the run rests on those
two numbers.

It ends with a verdict, and the verdict is sometimes **do not source this
segment**. Reasons: too few operators inside your size box, mostly sponsor-owned
already, no public ownership information, or no source that enumerates the
population. That verdict is worth more than a list.

**You approve:** the map and the verdict.

### 3. Discovery

It enumerates the population from the sources the map named. Licence rosters
first, then associations, exhibitor lists and dealer locators. Every row carries a
source string specific enough to re-run.

Then it deduplicates, applies only the geography and segment gates, and writes a
coverage log that names what the pull capped or missed.

**You approve:** the counts, the coverage log, and fifteen sample rows.

> Expect a chunk of rows with no website at all. Those are frequently the best
> rows on the list. A thin website is not a negative signal in this system, and
> the rule exists because breaking it inverts the result in exactly the market
> you are trying to reach.

### 4. Ownership, size and signals

Ownership first, from filings and registers, with the sponsor screen on every
row. Then revenue and EBITDA ranges with the basis attached. Then the platform or
add-on call. Then the four signal families.

Runs in batches of 20 to 30 with a report between each.

**You approve:** each batch.

> The most valuable line in this step is usually the list of companies that a
> sponsor already owns but that still describe themselves as family owned on
> their own website. Each one is a letter that does not get written to an owner
> who sold two years ago.

### 5. Ranking

It writes the rubric out in full — every criterion, the box section it came from,
the test, the bucket effect — and gets your approval **before ranking a single
row**.

Then it ranks every row in the same fixed order, and runs the four-part audit:
verify ten PRIORITY signals at their source URLs, pull twenty random PASS rows
and hunt for false negatives, re-screen the keep pile against sponsors, sanity
check the distribution.

**You approve:** the rubric. Then you get the ranked list and the audit.

### What you end up with

- `targets.csv` — every row ranked, with the rule that ranked it
- The PRIORITY rows summarised in chat, each with its role, its signal and an
  honest list of what is still unknown
- `market-map-[segment]-[date].md`
- `rubric-[segment]-[date].md`

For a 150 to 200 company run, expect 8 to 22 PRIORITY rows. If you get 60, the
rubric is flattering you and the system will say so.

---

# Working with the agents directly

You do not have to use the command. Talk to the agents.

```
> use buy-box-mapper to map the UK commercial laundry services market
  against my buy box

> ask buy-box-analyst to run the sponsor screen on everything in
  targets.csv

> buy-box-ranker, re-rank the list — I have widened the size box floor
  to $6M

> use buy-box-analyst on this CSV I already have, then rank it
```

That last one is common. If you already have a list from a database or a broker,
you can skip discovery entirely: drop your CSV in the folder, map your columns to
the template's, and run the analyst and ranker over it.

You can also call a single skill:

```
> run buy-box-market-map on Midwest commercial refrigeration service
```

---

# The safety rails

These are not configurable, and each one exists because breaking it produces a
specific and expensive failure.

**The principal-buyer gate.** If you earn a fee for arranging a transaction you
do not buy, the system stops and tells you to talk to securities counsel. It will
not research a target list on that basis, and saying it is fine does not change
the answer.

**Nothing writes without showing you first.** Every skill has a hard gate before
it writes to `targets.csv`.

**Unknown is not failed.** `Not found` revenue is not a failed size test.
`Not found` ownership is not a failed ownership test. Ranking gaps as negatives
systematically deletes the least-marketed companies from your list, which is to
say the proprietary ones.

**Estimates are labeled, always.** And a labeled estimate outside your size box
makes a row WATCH, never PASS. Only a verified figure excludes on economics.
Excluding a real target because a headcount guess landed 15 percent under your
floor is the most expensive routine error in origination, and it happens
silently.

**Sponsor-owned is always PASS.** The screen runs on every row, including the
ones that look obviously founder-owned.

**Signals are quoted verbatim or they do not exist.** No paraphrase inside
quotation marks, ever. A fabricated quote is the one error in this whole package
that reaches an owner.

**Public sources only.** Nothing behind a login that forbids it, nothing
paywalled without a licence, nothing that requires misrepresenting who you are.
No guessed email addresses — in fact, no email addresses at all, because contact
finding is not in this package.

**The audit runs every time and gets reported whether or not it is clean.**

---

# Troubleshooting

### `/skills` does not show the six skills

Check the files landed in the right place. Each skill needs to be its own folder
containing a `SKILL.md`:

```bash
ls ~/.claude/skills/
# buy-box-discovery  buy-box-intake  buy-box-market-map
# buy-box-ownership-and-size  buy-box-ranking  buy-box-signals

ls ~/.claude/skills/buy-box-ranking/
# SKILL.md
```

If you see a `skills` folder inside `skills`, you copied the folder instead of
its contents. Note the `/*` at the end of the copy command.

Restart Claude Code after copying.

### `/agents` does not show the three agents

Same check:

```bash
ls ~/.claude/agents/
# buy-box-analyst.md  buy-box-mapper.md  buy-box-ranker.md
```

These are flat `.md` files, not folders.

### `/map-buy-box` is not there

```bash
ls ~/.claude/commands/
# map-buy-box.md
```

Restart Claude Code. If it still does not appear, you can run the chain by
talking to the agents instead — see the section above.

### "It cannot find my references files"

The skills read `references/` from the cloned repo, not from your workspace
folder. Tell it where the clone is:

```
> the references folder is at ~/buy-box-mapper/references
```

Or copy the folder into your workspace. Either works.

### It keeps saying `Not found` instead of giving me data

Working as intended. A blank is honest; an invented ownership type or a made-up
revenue figure is not, and it silently corrupts every verdict downstream.

If it is `Not found` on almost everything, the usual cause is that the market map
came back without segment economics. Check the map's economics section. Without a
sourced revenue-per-head range there is no honest way to size anything.

### The ranking gave me almost no PRIORITY rows

Four usual causes, in order of likelihood:

1. **The signals pass has not run.** PRIORITY requires a signal. Without the
   signals step, everything clean lands at WATCH, which is correct
2. **Too many must-haves.** Twelve requirements means nothing survives. Three to
   five
3. **The size box is above the market.** The map will have told you this. Reread
   the size distribution section
4. **Discovery is aimed at the wrong population.** Over 70 percent PASS means
   fixing discovery, not the rubric

### The ranking gave me far too many PRIORITY rows

Above 25 percent means the rubric is flattering you or the signals are being read
generously. Check that `Not found` ownership rows are capped at WATCH, and reread
the `high` strength signals — a job posting is not a `high`.

### It classified a company as `Not found` ownership and I know the family owns it

Tell it, and tell it what the evidence is. A company saying "family owned" on its
about page is Tier 3 evidence at best, because companies keep that language for
years after a sale, and the system is deliberately strict about it. If you have
Tier 1 or Tier 2 evidence, it will take it.

### It refuses to write outreach

Correct. Outreach is not in this package. Contact finding, drafting and pipeline
are a different job with different rules.

### It stopped and asked about broker-dealer registration

Because section 1 of your buy box says you earn a fee for arranging transactions
you do not buy. That is a real regulatory question in the US and the rules differ
by state and by fee structure. Talk to securities counsel. If you are buying as a
principal, correct section 1.

### It is slow

A 200-company run with ownership research and signals is a few hours of
Claude Code working, not a few minutes. It is replacing roughly a fortnight of
associate time. Run it in batches and let it report between them.

### Windows path problems

Use `$HOME` in PowerShell, not `~`. Quote any path with a space in it. If a copy
silently does nothing, check you included the `\*` at the end of the source path.

---

# FAQ

### Do I need to pay for anything beyond Claude Code?

No. No database, no API keys, no data subscriptions. If you already pay for an
M&A database you can feed its export in as a starting list, but the whole design
assumes you do not have one.

### Why three buckets instead of a score out of 100?

Because a score invites an argument about whether a 71 beats a 68 and tells
nobody what to do on Monday. PRIORITY, WATCH and PASS each tell you exactly what
to do next.

### Why can it not find contact details or send the outreach?

Deliberately out of scope. This package does the part that costs a fortnight of
associate time: turning a mandate into a ranked list of companies worth calling.
Contact verification and owner outreach have their own rules — about guessed
email addresses, about what you may say to a founder, about what happens to a
reply — and a package that improvises them is worse than one that stops.

### What if I already have a list?

Skip discovery. Map your columns to `templates/targets.csv`, then run
`buy-box-analyst` and `buy-box-ranker` over it. Ranking somebody else's list
against your own rubric is one of the more useful things here, and the audit
usually finds something.

### Is my data safe?

Everything stays in local files on your machine. The `.gitignore` is set up to
keep your workspace out of version control. Do not put your workspace folder in a
public repository.

### Can I use this outside the US?

Yes, and the UK is in some ways easier: Companies House publishes accounts and
officer histories for free, which means more `verified` revenue figures and
Tier 1 ownership evidence. The EU varies by country. The map step will tell you
whether ownership information is publicly available in your geography before you
commit to a run.

### How many companies should I map at once?

100 to 300 for a focused mandate. Not thousands. A list of 5,000 unqualified rows
buries the dozen real conversations in noise, cannot be researched properly, and
tempts a bulk approach into a market where owners know each other and talk.

### Can I change the rules?

The buy box is yours — change it freely, and the system re-ranks. The files in
`references/` are the rules the skills enforce, and you can edit those too. Be
careful with four of them: unknown is not failed, estimates never produce a PASS
on their own, a thin website is not a negative signal, and signals are quoted
verbatim. Each of those protects you from a specific failure that is invisible
when it happens.

### Why does it keep telling me to run the market map first?

Because the map produces the segment economics that every revenue estimate rests
on, the source list discovery pulls from, and the consolidator list the sponsor
screen runs against. Without it, the run either stops or invents them.

### Three agents seems few compared to other packages

It is one job done properly rather than a whole origination desk. Buy box in,
ranked list out. If you want the full chain — contacts, warm paths, outreach,
sequencing, pipeline, and the maintenance pass that stops a list rotting — that
is a bigger package and a different repo.

---

# When you outgrow files

Files are the right answer for one mandate and a few hundred companies. Signs you
have outgrown them:

- More than one mandate running at once, with overlapping geographies
- More than about 500 live rows
- More than one person needing the same ranked list
- You want the list re-ranked on a schedule rather than on request
- You want the WATCH rows re-read every quarter automatically, because hiring
  signals expire at 90 days and a six-month-old ranking has a stale timing
  column

At that point you want a database, a scheduled re-read, and someone accountable
for the pipeline rather than the list.

---

# What's next

Run it on one segment. Not three. Get the box right, accept the map's verdict even
when it is unhelpful, and look hard at the audit — especially the false negatives
among the PASS rows, because that is where a real target hides.

Then take the PRIORITY rows and go and have the conversations. That part is still
yours.

---

Free and MIT licensed. Built by [Corebits](https://corebits.io).
