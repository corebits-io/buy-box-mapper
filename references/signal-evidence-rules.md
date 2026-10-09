# Timing Signal Rules — The Four Families, and What Counts as Evidence

Fit tells you whether a company belongs in the mandate. A timing signal tells
you why this quarter. The ranking rubric keeps them separate on purpose, and
PRIORITY requires both.

A signal is only a signal if it is **quoted verbatim, sourced to a URL, dated,
and rated honestly.** Everything else is a feeling about a company.

---

## The four families

### 1. Growth

The company is getting bigger in a way that changes the conversation.

- New site, depot, plant, clinic or region announced
- Capacity added: fleet, lines, bays, beds, machines
- A named large contract or framework award
- Headcount up materially against a stated earlier number
- A new service line or licence category

**Why it matters for an approach:** growth usually outruns the owner's systems.
It is the moment a founder starts thinking about whether the next stage is theirs
to fund.

### 2. Hiring

Who the company is hiring tells you what it is about to do.

- First CFO, finance director or controller
- First COO, general manager or operations director
- A corporate development, integration or M&A role
- A step change in volume of open roles
- Senior roles posted in a new geography

**Why it matters:** a first professional finance hire at a founder-owned company
is one of the strongest pre-process signals there is. Somebody has decided the
numbers need to be presentable.

### 3. Financing

Money arriving or being restructured.

- New debt facility, refinancing, or a new lender of record
- A minority or growth investment
- A sale-leaseback or property release
- New UCC filings or equivalent security registrations
- A grant, bond or public financing package

**Why it matters:** financing events put a valuation conversation on the table
and often come with a clock. They also tell you whether a sponsor is already
circling.

### 4. Leadership

The people who can sell are changing.

- Founder or owner stating age, succession, retirement or no next generation
- A title change: founder moving to chair, a non-family CEO appointed
- A death, illness or departure in the ownership group
- A long-tenured second generation taking over, or declining to
- A partner or shareholder exit

**Why it matters:** this is the family that produces the most actual
transactions, and the one most often mis-read. A quote beats an inference every
single time.

---

## Evidence tiers

| Tier | What it is | Usable? |
|---|---|---|
| **Tier 1** | A filing, register, licence record, court record, or official award notice | Yes, strongest |
| **Tier 2** | The company or the person saying it on the record: press release, interview, trade press quote, their own site, their own LinkedIn post | Yes |
| **Tier 3** | A dated third-party report naming its source | Yes, with the caveat recorded |
| **Tier 4** | An aggregator, a database field, an undated page, a "according to sources" line | No. Use only as a pointer to find Tier 1 to 3 |

Record the tier in `evidence_tier`. A signal resting on Tier 4 alone is
`Not found`, not `low`.

---

## Strength ratings

| Strength | Test |
|---|---|
| **high** | Tier 1 or Tier 2, inside the recency window, and the signal is about a decision rather than an atmosphere. Quotable to the owner without embarrassment |
| **medium** | Tier 1 to 3, inside the window, real but indirect. A first CFO hire with no stated reason sits here |
| **low** | Inside the window but thin: one job posting, a small headcount move, a vague quote |
| `Not found` | Nothing sourced and dated. The honest and common answer |

---

## Recency windows

Age the signal against its family, not a single global cutoff.

| Family | Window | After that |
|---|---|---|
| Hiring | 90 days | Expired. A six-month-old job posting is not a signal, it is a vacancy that was probably filled |
| Financing | 12 months | Downgrade one level |
| Growth | 12 months | Downgrade one level |
| Leadership | 24 months | Still usable. Succession moves slowly and an owner who said they had no successor two years ago probably still does not |

Write the evidence date to `evidence_date` in `YYYY-MM-DD`. A signal with no
date is `Not found`.

---

## Hard rules

**1. Quote the words. Never paraphrase into quotation marks.** If the source
says "we are exploring options for the next phase", that is the quote. Writing
"the founder is looking to sell" is a fabrication, and it is the kind that ends
up in an email to the founder.

**2. Every signal carries a working URL.** Not a domain, not a search result.
The page the words are on.

**3. One signal per row in `signal`, the best one.** Extras go in `notes`. A row
with five weak signals is still a weak row, and stacking them is how a WATCH
becomes a PRIORITY it has not earned.

**4. No signal is the normal answer.** Expect `Not found` on the majority of any
honestly researched list. A list where every row has a signal has invented some.

**5. Never infer succession from age alone.** A founder being 64 is not a
signal. A founder saying there is nobody in the family to take it on is.

**6. A signal never changes the fit verdict.** It changes the timing verdict
only. See the ranking rubric, hard rule 6.

**7. Public sources only.** Anything behind a login that forbids scraping,
anything paywalled you do not have a licence for, and anything that requires
pretending to be somebody else is out. The research ethics section of the setup
guide is not advisory.
