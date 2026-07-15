# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**What I did:**  Renamed save_to_watchlist() to add_to_watchlist(), and updated all calls to it to match the new name.
**How I verified:** I used VSCode's find all references feature.

## Comment 2 — Deduplication
**What I did:** Added code to handle deduplication case, checks if user already has film in their watchlist, raises error.
**How I verified:** With test cases created in test folder.

## Comment 3 — Missing test
**What I did:** Creaetd tests_watchlist.py and added nonexistent film raises, following same fixture and structure as the collection one in test_collection.py. 
**How I verified:** used pytest tests/test_watchlist.py -v , and checked that both test cases passed

## Comment 4 — Default visibility
**My position:**
**Reasoning:**
**Tradeoff acknowledged:**

## Comment 5 — Sort order
**My position:**
**Reasoning:**
**Engagement with reviewer's point:**

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->