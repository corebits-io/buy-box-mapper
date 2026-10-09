# Where the Companies Actually Are

A map is only as good as the population it enumerates. Bought lists and the
obvious M&A databases cover the same companies everybody else is calling — that
is precisely what makes them non-proprietary. The sources below are where the
rest live.

Work several angles per market. A list built from one source is that source's
list, with its coverage bias fully intact and invisible.

---

## Tier 1 — Statutory and regulatory

The best coverage that exists, and almost nobody works it properly.

- **Company registers.** Companies House (UK, free and complete, with accounts),
  US Secretary of State registries (per state, quality varies enormously), EU
  business and beneficial ownership registers, Canadian federal and provincial
  registries
- **Licensing boards.** Contractor, electrical, mechanical, plumbing, HVAC,
  pharmacy, healthcare facility, childcare, liquor, waste, transport. A state
  licence roster is often a complete list of the operators in a segment, with
  addresses and a named qualifying individual
- **Sector regulators.** CMS provider files, FDA registration, FAA and DOT
  registries, environmental permits, food handling registrations
- **Public contract awards.** Federal, state and municipal procurement portals,
  UK Contracts Finder, TED for the EU. A revenue floor and a customer list in
  one place
- **Court and filing records.** UCC filings naming lenders and sponsors,
  judgments, probate where it bears on ownership

## Tier 2 — Industry and association

- **Trade association member directories.** Frequently the highest-quality list
  of real operators in a niche, with the segment self-classified for you
- **Trade show exhibitor lists.** This year and the three before it. Exhibitors
  are operators spending money on growth, and past-year lists are badly
  undercovered
- **Certification and accreditation registers.** ISO, industry quality marks,
  manufacturer authorised-dealer lists
- **Buying groups, franchise and dealer networks**
- **Trade press directories, awards shortlists and fastest-growing lists**

## Tier 3 — Commercial and operational

- **Manufacturer and supplier dealer locators.** An underused route to a
  complete regional operator list
- **Insurance and bonding registers** where published
- **Job boards.** A company hiring five technicians has a revenue base, and the
  posting often states headcount and territory
- **Review platforms** for consumer-facing segments. Volume and tenure, never
  star ratings
- **Local business journals** and their annual regional rankings

## Tier 4 — Aggregators

Useful for cross-checking and for headcount. Never the spine of a list.

- **LinkedIn company search** — good for headcount and hiring, poor for small
  private operators with no page
- **Google Maps and local directories** — good for geographic completeness in
  physical-premises segments
- **Commercial M&A databases** — good for sponsor ownership, weak on the
  companies nobody has written about, and their revenue fields are estimates
  somebody else made

---

## Coverage bias, by source

Every source over-represents something. Name it in the coverage log.

| Source | Over-represents | Misses |
|---|---|---|
| Trade associations | Larger, joined-up, marketing-aware operators | The 40-year-old firm that never joined anything |
| Trade shows | Growth-minded, capex-spending firms | Steady service businesses with no growth agenda |
| LinkedIn | Younger firms, white-collar segments, urban | Trades, rural, and anybody over 60 who never made a page |
| Google Maps | Retail and physical premises | B2B firms in industrial units with no signage |
| M&A databases | Anything ever written about, anything sponsor-owned | Exactly the proprietary population you want |
| Licence rosters | Regulated activity only | Unlicensed adjacent services |

The companies that appear in **no** aggregator but **do** appear in a licence
roster are, disproportionately, the ones nobody has called.

---

## Working a source properly

1. Establish what the source's population actually is before pulling from it
2. Pull the whole segment, then filter. Never search and cherry-pick, which
   silently biases the list toward the well-named and the well-marketed
3. Record the source string per row in `source`, specifically enough that
   somebody else could re-run the same pull
4. Note what the pull capped or truncated. A 500-row export from a 1,200-row
   roster is a fact the coverage log needs
5. Cross-find. A company in three independent sources is a real company. One
   appearing in a single aggregator may be a duplicate, a defunct entity, or a
   holding shell

---

## Deduplication

Private company lists duplicate heavily, and the duplicates are not obvious.

Merge on **domain first**, then on **registry number**, then on normalised name
plus postcode. Watch for:

- Trading name versus registered name (`Smith Mechanical` / `J Smith & Sons Ltd`)
- The holding company and its operating subsidiary listed separately
- Branch offices of one company appearing as several companies in Maps
- Entity suffix noise: Ltd, Limited, LLC, Inc, Inc., Corp, Co
- Spelling variants in registry data, which is typed by hand more often than you
  would hope

Keep the merged row, record the other names in `notes`, and keep every source
string. A dedupe that silently discards a source string loses the cross-find
that made the row credible.

---

## Volume

**100 to 300 well-qualified companies for a focused mandate.** Not thousands.

A list of 5,000 unqualified rows is worse than 150 good ones. It buries the dozen
real succession conversations in noise, it cannot be researched properly, and it
tempts a bulk send into a market where the owners know each other and talk.
