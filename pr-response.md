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
**My position:** Keep public = True as default
**Reasoning:** A watchlist can be something users want to share (i.e. sharing lists with friends, it's social). If visibility defaults to private, the sharing capability wouldn't exist since most users might not go out their way to change the settings. By defaulting to public it allows this feature to work as intended (part of the social experience), so the user doesn't have to take extra steps when they want to share their list. 
**Tradeoff acknowledged:** Downsides include privacy concerns for users that might not have notice the visibility, to address this ideally the user should be made aware of this feature either when they first use the watchlist, and make an easy journey to the settings for it. 

## Comment 5 — Sort order
**My position:** Agree with comment, changed to date-added (Descending)
**Reasoning:** User's expectations are likely to be that watchlist would be ordered by recently added date rather than in alphabetical order (given standards across different platforms). Having it in alphabetical might surprise/bother some users, and might not be practical for this case (since it can also change at any time).
**Engagement with reviewer's point:** Agreed with reviewer's point, having ordered by date would meet user's expectation and is more useful, updated code to reflect it. 

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->