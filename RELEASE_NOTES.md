# Release Notes

Covers Desktop/Web **v6.9.6 → v6.10.3** and Mobile **v2.6.2 → v2.7.0** (2026-09-09 to 2026-09-18).

This file is duplicated in the companion [BoardGameLibrary](https://github.com/ballewcifer/BoardGameLibrary) repo (Desktop/Web) since most of this window's work spanned all three platforms.

---

## BGG collection status (Owned / Wishlist / For Trade / etc.)

- Sync now imports your BoardGameGeek collection's real status per game, not just what you own — reviewable and overridable on every platform's Add/Edit Game screen, and shown on the detail view when it isn't the default "Owned." A manual override is protected from being silently overwritten by the next sync. (Mobile v2.6.2, Desktop v6.10.2, Web v6.10.2)
- **Mobile**: the Games tab's collection-status filter is now multi-select — tap any combination of Owned/Wishlist/For Trade/etc. on or off, instead of picking one at a time. It also now **defaults to "All"** instead of "Owned," so newly-synced wishlist/for-trade items aren't hidden until you go looking for them; the "All" chip is listed first. (v2.6.6, v2.6.7)
- **Mobile**: only owned games are ever loanable — the "Available" badge, the Available filter, "only available" in the random picker, and Check Out no longer apply to non-owned games. Non-owned games show their real status instead (Wishlist, For Trade, …), each with its own color, applied consistently everywhere a status appears. (v2.6.5)
- **Mobile**: "Clear Collections" now removes all synced games regardless of status, not just owned ones. (v2.6.3)

## Sync with BGG — now consistent everywhere (Mobile)

The Dashboard's "Sync with BGG" used to be a stripped-down, username-only shortcut with no password field and no way to claim a collection — different from the full version on the Games tab. Both entry points now share one component and offer the exact same fields and behavior, including the optional "claim this collection as my own" step. (v2.6.7)

## Friends (Mobile)

- **One sheet for adding a friend everywhere.** Adding a friend, checking a game out to someone new, and logging a play with a new player now all ask for first and last name the same way — previously Check Out and Log Play took one typed string and guessed where to split it. (v2.6.9)
- **Edit friends**: tap a friend on the Friends tab to change their name or add a BoardGameGeek username later. The Add Friend sheet on that tab also has an optional BGG username (reference only — no collection import yet). (v2.6.9)
- **Claiming your collection when you sync no longer asks for your name** and no longer creates a friend as a side effect — it's tied to the BGG username you're syncing with. Friends are only created from Add Friend, Check Out, or Log Play. (v2.6.8)

## Backup & restore (Mobile)

- Backups now include **manually added games**, which have no BoardGameGeek record to re-sync from and were previously lost on a reinstall. Older backup files still import; they just don't contain manual games. (v2.6.10)
- The Dashboard now explains the restore order: export a backup and save it off the phone before reinstalling; after reinstalling, **sync with BoardGameGeek first, then import** — plays, loans, and per-game details only attach to games already in your library. (v2.6.10)
- Friends' BGG usernames are included in backups. (v2.6.9)

## Adding games

- **Mobile**: a genuine manual-entry flow ("Add Manually") where every field is editable by hand, not just whatever BGG provides — separate from "Add from BGG" search. Both flows, plus BGG sync, let you set the collection status up front. (v2.6.3)
- Fixed a bug where BGG search could fail with an authentication error after certain updates — an embedded app token now always takes priority over a stale one from an older build. (Mobile v2.6.3)

## Cooperative / Competitive game type

Desktop and Web now match the mobile app: auto-detected from BoardGameGeek's mechanics data on every sync or add, editable per game, usable as a filter and in the random-game picker, and protected from being overwritten by a future sync once manually set. (Desktop/Web v6.10.0)

## Expansions link to their base game

Desktop and Web now match the mobile app: an expansion's page shows "Expansion for X," and the base game's page shows "Expansions You Own." (Desktop/Web v6.10.1)

## Complete backups

Backup & restore now includes custom cover photos, best-player counts, and Cooperative/Competitive settings — previously left out of exported backups. (Mobile — already covered; Desktop/Web v6.10.1)

## Checkout friend picker

Desktop and Web's Check Out screen now use the same type-or-pick autocomplete friend picker that Log Play already used, instead of a plain dropdown — a new name auto-creates the friend at checkout time. Also fixed both platforms hiding Check Out entirely when zero friends existed yet. (Desktop/Web v6.9.6)

## Bug fixes

- Clearing a collection that was synced from a BGG username now also forgets that username, so a later manual sync can't silently recreate the collection you just cleared. (Desktop/Web v6.9.7 — matches an earlier mobile fix)
- **Mobile**: fixed a launch crash on iOS caused by a couple of native modules being built against mismatched versions of a shared library; also fixed "Set Image" silently missing a required permission description that would have crashed it on iOS regardless. (v2.6.2)
- **Mobile**: fixed a FlatList layout bug where a single search/filter result stretched to fill the whole row instead of sizing to one column. (v2.6.5)
- Fixed `upsertGame` occasionally being able to silently wipe an existing game's real BGG status back to unset. (Mobile v2.6.3/v2.6.5, matching fix applied on Desktop/Web)
- **Mobile**: fixed the on-screen keyboard covering sheets on Android. The Friend picker in Check Out and Log Play was the worst case: its "add a new friend" field sat at the very bottom of a short sheet, so opening the keyboard hid the whole sheet. Every sheet and form with a text field now lifts above the keyboard, the picker's add field moved to the top, and the shared sheets leave room for the phone's navigation bar. Also, tapping a button, list row, or game card while the keyboard was open only closed the keyboard first and needed a second tap; that now works on the first tap everywhere, and the Check Out and Edit Checkout sheets scroll instead of cutting fields off. (v2.7.0)
- Fixed the Android keyboard-close animation causing modal sheet content to visibly compress and overlap for a frame before snapping into place — was most visible in the Sync with BGG sheet, then found and fixed across every remaining modal that had it. (Mobile, mid-window)

## Accessibility

A pass across every platform:

- **Mobile**: added missing screen-reader labels/roles to icon-only buttons, search fields, and save/cancel buttons; fixed a checkbox/switch role mismatch; enlarged an under-sized touch target; announced the disabled state on "saving…" buttons; gave the iOS date-picker sheet the same Escape/back-close behavior every other modal already had. (v2.6.7)
- **Desktop**: every dialog now closes on Escape (previously only one did); enlarged a too-small touch target on the filter-chip dismiss button. (v6.10.3)
- **Web**: modal dialogs now trap Tab focus instead of letting it escape into the page behind them; fixed a multi-select checkbox that was invalid HTML (nested inside a link, confusing keyboard/screen-reader focus order); fixed a toggle button's screen-reader label going stale when its visible text changed; added missing screen-reader text to a favorite-star badge; added a visible "Overdue" tag next to the Dashboard's overdue rows, which previously relied on red text color alone; fixed the win-leaderboard's medal icons replacing the numeric rank instead of decorating it, and made the leaderboard toggle announce its expanded/collapsed state. (v6.10.3)

## Store distribution (Mobile)

**Correction from the previous notes**: store submission is **not** fully automated. CI (triggered by a `store-v*` tag) builds and signs the Android App Bundle and iOS build and attaches them to a GitHub Release — it does not upload them to Google Play or App Store Connect. That upload step is still a manual `eas submit` run per platform, using credentials stored in EAS (or a local key file as a fallback). Apple's actual "Submit for Review" click, to publish a version live, is a separate manual step in App Store Connect that nothing in this pipeline performs.
