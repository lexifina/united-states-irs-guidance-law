# How this repository was made

Made on 2026-11-09 by Claude Code (Claude Opus 5.5, `claude-opus-5-5`), which wrote the scripts and ran them. No AI model
wrote, edited or summarised any item's text, and none chose a date.

1. `python fetch.py`: every Internal Revenue Bulletin issue from 1996, as PDF (`https://www.irs.gov/pub/irs-irbs/irbYY-NN.pdf`)
   and, from 2004, as a web page (`https://www.irs.gov/irb/YYYY-NN_IRB`), one request at a time a second apart, with curl.
   irs.gov's robots.txt disallows only its /core/ and /profiles/ folders and some search paths; nothing fetched here.
   data/index.json records each file's URL, sha256 and fetch time.
2. `python -X utf8 build.py items`: each issue's items, split at their headings ("Rev. Proc. 2024-1"), from the web page
   or, before 2004, the PDF's text layer (PyMuPDF 2.0); an item printed
   again in a later issue keeps its first printing; the effective-date sentence and the "is superseded/modified" lines
   read by pattern.
3. `python -X utf8 build.py repo <out> --today 2026-11-09`: one commit per item with git fast-import, then this
   documentation.
