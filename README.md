# Funded Companies Hiring: Python example

**Funded Companies Hiring - Raises, Jobs and Contacts.** Companies that just raised money (SEC Form D), with their open roles and business contacts, as a new-only monitor. Price, example input and output, and FAQ: [Funded Companies Hiring on the Aurelix tools site](https://aurelix-solutions.github.io/tools/funded-companies-hiring/). Run it on the Apify Store: [apify.com/aurelix/funded-companies-hiring](https://apify.com/aurelix/funded-companies-hiring).


A small, runnable example for [Funded Companies Hiring](https://apify.com/aurelix/funded-companies-hiring), an Apify Actor by Aurelix.

[![Funded Companies Hiring: 75-second demo video](https://api.apify.com/v2/key-value-stores/twkCCtTWzsi8fVbx5/records/funded-companies-hiring-demo-thumb-v1.png)](https://api.apify.com/v2/key-value-stores/twkCCtTWzsi8fVbx5/records/funded-companies-hiring-demo-v1.mp4)

**[▶ Watch the 75-second demo](https://api.apify.com/v2/key-value-stores/twkCCtTWzsi8fVbx5/records/funded-companies-hiring-demo-v1.mp4)**

## What it does

Funded Companies Hiring joins three public sources into one row per company. It reads the official SEC EDGAR Form D filings, the notice US companies file within 15 days of first selling shares, notes or SAFEs in a private round, and drops investment funds, SPVs and real-estate vehicles. For each operating company it confirms the website against the filing, finds the company's own public job board and reads every open role, then (optionally) reads the company's own contact, about and team pages for business emails, phones, contact pages, social links and the leaders it names there. Within each filing day the biggest raises are checked first. Turn on 'Only new since last run' and schedule it daily: later runs return only companies that are new, plus companies you already have whose job board now shows roles that were not there at the last check.

## Why this over alternatives

Compared with the alternatives a buyer would otherwise use (the same table is on the Store page):

| | **This Actor** | conserving_celerytop/raised-and-hiring-signal-api | Crunchbase Pro + Apollo Basic |
|---|---|---|---|
| **Price, free plan** | $20 per 1,000 hiring companies; contacts $10 per 1,000 when found | $30 per 1,000 companies with open jobs | $99 a month (Crunchbase Pro, monthly) + $59 a user a month (Apollo Basic, monthly) |
| **Price, paid plans** | $16 per 1,000; contacts $8 per 1,000 | $27 to $21 per 1,000 | same subscriptions; yearly billing is cheaper |
| **Start fee per run** | $0.025 | $0.00005 | none (subscription) |
| **Funding source** | SEC Form D (official, US) | SEC Form D | Crunchbase's own database (global, with investors and round names) |
| **Job-board systems read** | 7: Greenhouse, Lever, Ashby, SmartRecruiters, Workable, BambooHR, Workday | 3: Greenhouse, Lever, Ashby | not part of either product's job-board reading |
| **Every open role with title, department, location and link** | ✓ | count and top titles | ✗ |
| **Company emails, phones and contact pages** | ✓ from the company's own site | not stated | Apollo: from its contact database, on credits |
| **New since last run: new raises and new roles only** | ✓ | not stated | separate saved searches in each tool |
| **Investor names and round stage (seed, Series A)** | ✗ (Form D has none) | ✗ | ✓ Crunchbase |
| **Coverage outside the US** | ✗ (US Form D filers only) | ✗ | ✓ |

- One run replaces a funding database, a job-board scraper and a contact tool joined by hand.
- Reads seven job-board systems including Workday; the other Form D plus jobs Actor we found reads three.
- $20 per 1,000 hiring companies, against $30 per 1,000 for the other Form D plus jobs Actor.
- Monitor mode remembers every role ID, so a daily run alerts only on new raises and new roles.
- Business contacts only: company mailboxes, phones, contact pages and leaders the company names itself.
- Funds, SPVs and real-estate vehicles removed; websites confirmed against the filing's city or phone.

## When to use it

- SDRs and account executives: reach companies in the weeks after they raise, when budgets open and teams grow
- Recruiters and staffing agencies: pitch funded companies that are already hiring for roles you fill
- Agencies (dev shops, design, marketing, HR, payroll, office space): find companies whose open roles show the need you serve
- Founders and investors: watch who raised in your sector and what they hire for next
- Sales ops: feed a CRM or Clay table with new raises plus hiring signals every morning

## Input example

```json
{
  "daysBack": 7,
  "sectors": [
    "technology"
  ],
  "maxResults": 25,
  "enrichContacts": true
}
```

Turn on `"incremental": true` and schedule the run daily to get only newly funded companies and companies whose job board shows new roles; add `slackWebhookUrl` for a plain-language digest.

## How to run

1. Get an Apify API token from Apify Console (Settings, API & Integrations).
2. Install and run:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
export APIFY_TOKEN=your_token_here
python main.py
```

The script starts a run of `aurelix/funded-companies-hiring`, prints each company's one-line summary and website, and writes every result to `results.csv`. Lists and nested objects (roles, contacts) are stored in the CSV as JSON text. Each run is billed to your Apify account (see Pricing below).

## Sample output

One record from a real run (roles shortened to 2):

```json
{
  "alert_type": "newly_funded",
  "summary": "Legora, Inc. raised $220.8M and has 312 open roles on Ashby, mostly Go To Market (GTM) and Legal Engineering.",
  "company_name": "Legora, Inc.",
  "cik": "0002071663",
  "entity_type": "Corporation",
  "year_of_incorporation": 2023,
  "city": "Dover",
  "state": "DE",
  "state_name": "Delaware",
  "industry_group": "Other Technology",
  "sector": "technology",
  "accession_number": "0002071663-26-000002",
  "form_type": "D",
  "filing_date": "2026-11-04",
  "filing_url": "https://www.sec.gov/Archives/edgar/data/2071663/000207166326000002/0002071663-26-000002-index.htm",
  "date_of_first_sale": "2026-10-20",
  "total_offering_amount": 550000000,
  "total_amount_sold": 220820026,
  "total_remaining": 329179974,
  "investors_count": 44,
  "securities_offered": [
    "Equity"
  ],
  "federal_exemptions": [
    "06b"
  ],
  "revenue_range": "Decline to Disclose",
  "website": "https://legora.com/",
  "domain": "legora.com",
  "is_hiring": true,
  "job_board": "Ashby",
  "job_board_url": "https://jobs.ashbyhq.com/legora",
  "careers_url": "https://legora.com/careers",
  "open_roles_count": 312,
  "roles_complete": true,
  "departments": [
    {
      "name": "Go To Market (GTM)",
      "open_roles": 56
    },
    {
      "name": "Legal Engineering",
      "open_roles": 55
    },
    {
      "name": "Engagement",
      "open_roles": 38
    },
    {
      "name": "People",
      "open_roles": 37
    },
    {
      "name": "Engineering",
      "open_roles": 33
    }
  ],
  "top_locations": [
    {
      "name": "New York City",
      "open_roles": 94
    },
    {
      "name": "Stockholm HQ",
      "open_roles": 60
    },
    {
      "name": "London",
      "open_roles": 39
    },
    {
      "name": "San Francisco",
      "open_roles": 16
    },
    {
      "name": "Denver",
      "open_roles": 13
    }
  ],
  "seniority_mix": [
    {
      "level": "mid",
      "open_roles": 119
    },
    {
      "level": "manager",
      "open_roles": 81
    },
    {
      "level": "senior",
      "open_roles": 43
    },
    {
      "level": "director",
      "open_roles": 25
    },
    {
      "level": "executive",
      "open_roles": 20
    },
    {
      "level": "staff_principal",
      "open_roles": 12
    },
    {
      "level": "entry",
      "open_roles": 12
    }
  ],
  "remote_share": 0,
  "new_roles_count": null,
  "new_roles": null,
  "roles": [
    {
      "role_id": "ashby:legora:71d649a0-542c-4852-b050-a06f07d66426",
      "title": "Director of Revenue, Federal",
      "department": "Go To Market (GTM)",
      "seniority": "director",
      "locations": [
        "US - Remote",
        "Remote, Remote, United States"
      ],
      "countries": [
        "US"
      ],
      "remote": false,
      "posted_at": "2026-11-04T20:30:30Z",
      "url": "https://jobs.ashbyhq.com/legora/71d649a0-542c-4852-b050-a06f07d66426"
    },
    {
      "role_id": "ashby:legora:d43c0032-0fa5-4e7c-90de-1d4bba181016",
      "title": "Engagement Manager - Copenhagen",
      "department": "Engagement",
      "seniority": "manager",
      "locations": [
        "Copenhagen",
        "Copenhagen, Capital region of Denmark, Denmark"
      ],
      "countries": [
        "DK"
      ],
      "remote": false,
      "posted_at": "2026-11-04T16:01:07Z",
      "url": "https://jobs.ashbyhq.com/legora/d43c0032-0fa5-4e7c-90de-1d4bba181016"
    }
  ],
  "roles_truncated": true,
  "contacts": {
    "emails": [
      {
        "email": "contact@legora.com",
        "source_url": "https://legora.com/contact-us"
      },
      {
        "email": "press@legora.com",
        "source_url": "https://legora.com/contact-us"
      },
      {
        "email": "support@legora.com",
        "source_url": "https://legora.com/contact-us"
      }
    ],
    "phones": [],
    "contact_pages": [
      "https://legora.com/contact-us"
    ],
    "social_profiles": [
      {
        "network": "linkedin",
        "url": "https://www.linkedin.com/company/wearelegora",
        "source_url": "https://legora.com/"
      },
      {
        "network": "x",
        "url": "https://x.com/WeAreLegora",
        "source_url": "https://legora.com/"
      },
      {
        "network": "youtube",
        "url": "https://www.youtube.com/@WeAreLegora",
        "source_url": "https://legora.com/"
      },
      {
        "network": "instagram",
        "url": "https://www.instagram.com/wearelegora",
        "source_url": "https://legora.com/"
      }
    ],
    "decision_makers": []
  },
  "source_url": "https://www.sec.gov/Archives/edgar/data/2071663/000207166326000002/0002071663-26-000002-index.htm",
  "scraped_at": "2026-11-05T07:01:06Z"
}
```

## Export to CSV

`main.py` writes `results.csv` with the `csv` module. You can also download any run's results directly:

```
https://api.apify.com/v2/datasets/<datasetId>/items?format=csv&clean=true
```

Send your token in an `Authorization: Bearer <token>` header if the dataset is not readable without one. Other formats: `format=json`, `format=xlsx`.

## n8n

- Apify node: choose "Run an Actor", enter `aurelix/funded-companies-hiring`, paste the input above, then read the run's dataset items.
- Or use the Actor's own Slack/webhook digest: set `webhookUrl` to an n8n Webhook node URL and each run that finds something posts its summary and top 10 companies as JSON.

## Limits

- US Form D filers only; no investor names, no round name (seed, Series A), and companies that raise without filing a Form D are missing.
- Websites are found only when the company name works as a .com, .ai, .io or .co domain and the site shows the filing's city or phone; most small issuers get none and are not returned.
- Open roles come only from Greenhouse, Lever, Ashby, SmartRecruiters, Workable, BambooHR and Workday boards linked from or named like the company's site; other systems and home-made careers pages give no roles.
- A job-board role marked remote in its location text but not in the board's remote flag shows remote false; check `locations` too.
- Workday boards are read up to Workday's 2,000-role search limit; roles_complete is false when a board was read only partly.
- Monitor mode re-checks the boards of the 50 most recent companies it returned, for 'Watch new roles for N days'. A funded company returned without a job board is not re-checked later, so a company that opens its board after its first run is not reported.
- Contacts come only from what the company publishes on up to 5 pages of its own site; sites that block crawlers in robots.txt are skipped.
- Days are EDGAR filing dates counted back from today in UTC, at most 30; amounts are copied as filed, so placeholder values such as $1 appear when the company entered them (the summary then says 'filed a Form D' instead of an amount).

## Pricing

At the time of writing:

| Event | Free plan | Paid plans (Bronze, Silver, Gold) |
|---|---|---|
| `company-result` | $20.00 per 1,000 companies | $16.00 per 1,000 companies |
| `contact-result` | $10.00 per 1,000 companies with contacts | $8.00 per 1,000 companies with contacts |
| `apify-actor-start` | $0.025 per run | $0.025 per run |

You pay one company-result per company returned with its open roles. Funded companies whose website or job board could not be found are not charged (with 'Hiring companies only' on, the default), nor are filings outside your filters, funds, suppressed names or anything returned before in monitor mode. A contact-result is charged only for a company whose website gave at least one email, phone, contact page, social link or named leader. In monitor mode a tracked company whose board shows new roles is one company-result.

Check the [Store page](https://apify.com/aurelix/funded-companies-hiring) for current prices.

## Links

- Actor: https://apify.com/aurelix/funded-companies-hiring
- Questions, bugs and feature requests: the Issues tab on the Store page.

## Licence

The example code in this repository is released under the MIT licence (see `LICENSE`). The Actor itself runs on Apify and is billed through your Apify account.
