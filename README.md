# SEC IPO Registration Tracker

Track new SEC Form S-1 filings — the registration statement a company
files with the SEC ahead of a US initial public offering — via the
official [EDGAR full text search](https://www.sec.gov/edgar/search/)
API. Search by keyword, or leave blank for all new S-1 filings
market-wide.

Built for finance, media, and deal-tracking teams who want to catch a
new IPO registration on day one instead of finding out from a news
headline.

## Input

```json
{
  "keyword": "",
  "includeAmendments": false,
  "daysBack": 30,
  "maxResults": 50
}
```

| Field | Type | Description |
|---|---|---|
| `keyword` | string | Free-text search across the filing, matching the registrant's name and filing text. Leave blank for all new S-1 filings market-wide. |
| `includeAmendments` | boolean | By default only original S-1 filings are returned (new IPO registrations). Turn this on to also include S-1/A amendments to already-filed registrations. Default `false`. |
| `daysBack` | number | How many days back from today to search, by filing date. Default `30`, max `120`. |
| `maxResults` | number | Maximum number of filings to return, most recently filed first. Default `50`, max `100`. |

## Output

One record per filing:

```json
{
  "accessionNumber": "0001731122-26-001117",
  "form": "S-1",
  "isAmendment": false,
  "registrantName": "SPLASH BEVERAGE GROUP, INC.",
  "registrantCik": "0001553788",
  "registrantTickers": "SBEV",
  "filingDate": "2026-08-20",
  "businessLocation": "Fort Lauderdale, FL",
  "incorporatedIn": "NV",
  "sicCode": "2080",
  "filingUrl": "https://www.sec.gov/Archives/edgar/data/1553788/000173112226001117-index.htm"
}
```

`registrantTickers` is only present if the registrant already has a
listed ticker at filing time (common for a rights offering or an
already-public company's follow-on S-1); a genuinely new pre-IPO
company will have this as `null`.

## How it works

Direct calls to the official SEC EDGAR full text search API
(`efts.sec.gov`) — no proxy, no key, no scraping. Same proven
mechanism as this portfolio's other SEC filing actors (8-K, Form D,
13D/13G, 13F), applied to a new filing type.

## Pricing note

Billed per **search** (one run), not per filing returned.

## Related products

- [SEC 8-K Material Event Tracker](https://github.com/timmKal01/sec-8k-material-event-tracker)
- [SEC 13D/13G Ownership Tracker](https://github.com/timmKal01/sec-13d-ownership-tracker)
- [SEC 13F Institutional Holdings Tracker](https://github.com/timmKal01/sec-13f-institutional-holdings-tracker)
- [Form D Fundraising Tracker](https://github.com/timmKal01/form-d-fundraising-tracker)
