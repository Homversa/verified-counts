# Verified Company Counts by City and Trade

How many home service companies pass license verification in each US city and trade, checked
against the state register that issues the credential for that trade.

**Version of 2026-09-11.** 15,099 rows, one per published city and trade: 384,462 verified company
records across 3,106 cities, 10 states, 28 trades and 18 registers.

Canonical page, always the newest version: https://homversa.com/data/verified-counts

## Why this exists

Nobody publishes counts of licensed companies per city. State registers publish licenses, not
geography; trade associations publish membership, not licensure. This dataset is the join: for
each city and trade, how many companies hold a current credential in the register that governs
that trade, with the register named on every row so a claim can be checked at its source.

It is the number behind every page on homversa.com, published once so it can be cited without
reading thousands of pages.

## What a row means

One row is one city and trade combination that the site publishes.

| Column | Meaning |
|---|---|
| `state` | Two-letter US state code. |
| `city` | City as the register spells it, normalized to the site's slug set. |
| `county` | County or county-equivalent containing the city. Virginia's independent cities and Connecticut's planning regions carry their own qualifiers. |
| `trade` | The trade, in the site's vocabulary (28 values). |
| `register` | The register the count was checked against, for example CSLB for California contractors or TDLR for Texas. |
| `verified_companies` | Companies with a current credential in that register, at an address in that city, for that trade, on the verification date. |
| `listed_companies` | How many of them the site shows on the page, capped at 10. Always less than or equal to `verified_companies`. |
| `monthly_searches` | A third-party keyword-tool estimate. See the warning below; do not use this column for research. |
| `page_url` | The page on homversa.com that publishes this combination. |

## Method

A company counts when it holds a current credential in the named register on the verification
date. It does not count because it bought a listing, because none are for sale.

A city and trade is published only where at least three companies pass verification. Combinations
below that bar are **absent from this file rather than present with a small number**. That is the
single most important thing to understand before using it: the file is not a complete grid of
cities by trades, and a missing row does not mean zero.

## What this data does not say

- **It is a floor, not a census.** It counts companies whose credential could be matched to a
  current record. Matching is imperfect, so the true licensed population is at least this large
  and probably larger.
- **It says nothing about quality or volume.** Not how many jobs a company takes, not how well it
  works, not whether it is accepting customers.
- **Two versions are two snapshots.** The counts change whenever a register is re-ingested, and
  the version date in the citation moves with them. Never compare a number from one version
  against a number from another and call the difference a trend.
- **Do not use `monthly_searches` for research.** It is a keyword-tool estimate carried for the
  site's own internal sorting, and the site's own measurement found it unreliable: pages the tool
  marked as zero-demand produced roughly twice the search impressions of the pages it marked as
  in-demand. It is included for completeness and transparency, not because it is good.

## Two structural caveats that will otherwise mislead you

**Florida is county-lens.** Florida publishes one principal city per county and folds the other
cities of that county into it, because its register records a contractor's address at a county
level that does not map cleanly to municipalities. So a Florida row's `verified_companies` covers
the county, while the `city` names the principal city. Dividing a Florida count by that one city's
population overstates density several-fold. If you are computing anything per capita in Florida,
use county population.

**Texas roofing is not a state license.** Texas licenses no roofers at all. Its roofing rows are
checked against the Roofing Contractors Association of Texas, which is a voluntary membership, so
a Texas roofing count measures who joined an association, not who may legally roof. It is not
comparable with Florida roofing, which is a state license. The `register` column names which is
which on every row; read it before comparing states.

## Files

- `verified-counts.csv` - the data. UTF-8, comma-separated, two leading comment lines beginning
  with `#` that carry the version date and the license, then a header row.
- `LICENSE` - CC BY 4.0.
- `README.md` - this file.

## Citation

> Homversa (2026). *Verified Company Counts by City and Trade*, version of 2026-09-11.
> https://homversa.com/data/verified-counts. CC BY 4.0.

Cite the version date. Two citations with different dates are two different snapshots.

## License

Creative Commons Attribution 4.0 International (CC BY 4.0). Free to use, including commercially,
with attribution and a link.

## Corrections

A wrong row is worth reporting and will be fixed: corrections@homversa.com, or the form at
https://homversa.com/contact. The underlying registers are public, so a correction can usually be
checked at its source in minutes.

## Source registers

Every count names its register in the `register` column. The full list of registers, what each
covers, and how often each is re-checked is published at https://homversa.com/methodology.
