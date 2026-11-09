# IRS guidance as a git history

Part of [lexifina/global-law](https://github.com/lexifina/global-law): the guidance the Internal Revenue Service publishes
in the Internal Revenue Bulletin, which global-law reads at `united-states/federal/irs-guidance/`. One file and one commit
per item: 10,111 items from bulletins 1996-01 to 2026-46 (1,306 × Treasury decision (final or temporary regulations), 2,074 announcements, 2,467 notices, 1,114 × notice of proposed rulemaking (proposed regulations), 1,697 revenue procedures, 1,453 revenue rulings).

| Question | Command |
|---|---|
| An item | `cat rev-proc/2024/2024-001.md` (or `grep 'Rev. Proc. 2024-1' item-index.tsv`) |
| Everything published in a bulletin | `git log --grep='Bulletin: I.R.B. 2024-01'` |
| What a later item did to an earlier one | `git log --grep='Effect: Rev. Proc. 2023-1'` |
| Items in force in a window | read the `In-force:` trailer: `git log --format='%(trailers:key=In-force,valueonly,separator=) %an'` |

## Dates

Each commit is dated the day the item took effect when the item says so in one sentence of its own ("This revenue
procedure is effective January 1, 2025") and that day is within a year of its bulletin and not after 2026-11-09
(2,031 items); otherwise the day of the bulletin that published it. `In-force-basis:` says which, and `Published:`
always gives the bulletin's day. Many items apply to taxable years, transactions or filings rather than from a day; the
item's own words decide, and the file keeps them.

## What it is and is not

Each item is kept as first published. When a later item modifies, supersedes, obsoletes or revokes it, that later item
is its own commit and names the earlier one (`Effect: Rev. Proc. 2023-1 superseded`); the earlier file is not changed.
Revenue rulings and revenue procedures are the IRS's published positions; they are not statutes or regulations
(regulations are in the CFR, `united-states/federal/cfr`). Treasury decisions and proposed regulations are kept as the
bulletin prints them. Before 2004 the bulletin is published only as PDF: those items are read from the PDF's own text
layer, one text block per line in reading order, which on some two-column pages interleaves the columns
(`source` ends in `.pdf`); read the PDF for anything that matters.

## Source

The Internal Revenue Bulletin on irs.gov: each weekly issue's web page (`https://www.irs.gov/irb/<YYYY-NN>_IRB`), and
before 2004 its PDF (`https://www.irs.gov/pub/irs-irbs/irbYY-NN.pdf`). Works
of the US Government, in the public domain (17 U.S.C. §105). Text is the bulletin's own, one paragraph or table row per
line; nothing summarised or rewritten.
