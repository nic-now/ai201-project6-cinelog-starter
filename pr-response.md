# PR Response Doc — CineLog Watchlist Feature

## AI Usage
Used Claude to understand the codebase at the start (what files and functions did before touching them), help write the test file following the same structure as test_collection.py, and check logic on the deduplication code. For Comment 4, I asked it to lay out the tradeoffs between the two visibility options, the position/ reasoning in my response is my own but I used the output to make sure I wasn't missing anything.

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
**What conflicted:** .gitignore had a conflict since both branches added similar entries.
**How I resolved it:** Kept entries from both sides and ran `git rebase --continue`. Also updated `WatchlistEntry.film_id` in models.py from integer to UUID to match the refactor on main, and fixed the stale docstring in watchlist_service.py.
**How I verified no conflict remains:** `pytest tests/test_watchlist.py -v` passed, no merge commits in history.

## PR Description
This PR adds a watchlist feature where users can save films they want to watch later, separate from their collection (films already watched). Users can add a film, view their full watchlist, and each entry tracks when it was added and whether it's public or private.

Visibility defaults to public since the watchlist is meant to be social and defaulting to private would mean most users never share their list without realizing there's an option. Sort order is newest first, which matches how the collection works and what users would expect.

To test manually: add a film via POST to `/watchlist/<user_id>/add` with a valid `film_id` and confirm a 201 response, try adding the same film again and confirm a 409, try an invalid film_id and confirm a 404, then GET `/watchlist/<user_id>` and confirm films come back newest first. Run `pytest tests/test_watchlist.py -v` to confirm both tests pass.