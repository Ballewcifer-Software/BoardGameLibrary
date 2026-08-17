# Release Notes

Covers Desktop/Web **v6.8.4 → v6.9.0** and Mobile **v2.1.8 → v2.2.8** (2026-06-22 to 2026-08-04).

---

## Bulk editing & advanced filtering

- **Desktop**: the Games table now supports multi-row selection with a right-click bulk action to mark/clear "Has 3D Insert" across selected games. (v6.8.4)
- **Web**: added a "Select" mode on the Games grid with per-card checkboxes and the same bulk 3D-insert action. (v6.8.4)
- **Mobile**: long-press a game card to enter multi-select mode, then bulk mark/clear "Has 3D Insert." (v2.1.8)
- **Mobile**: added a full advanced-filters sheet — players (supports/exact), best-at, play time, complexity, tags, expansions, has-insert — matching Desktop's filter bar. Fixed a follow-up layout bug where the new Filters button broke the quick-filter row. (v2.2.2, v2.2.3)
- **Desktop & Web**: Members, Checkout History, and Play Log tables are now sortable by clicking any column header (previously only the Games table supported this). Sorting by a combined "Name" column correctly sorts by last name, and date columns sort chronologically regardless of display format. (v6.8.8)

## Checkout history

- **Web**: double-click a row in Checkout History to open the edit dialog (Desktop already supported this). (v6.8.5)
- **Mobile**: double-tap a checkout card to edit it, and fixed a bug where editing the return date silently discarded the time-of-day. (v2.1.9)

## Data integrity fixes

- **Mobile**: fixed a bug where syncing with BoardGameGeek could silently wipe a game's personal rating, comment, and "best at N players" note — these fields were never provided by BGG's sync data but were being overwritten anyway. Also fixed BGG-provided min/max playtime data being fetched but silently discarded. (v2.2.1)
- **Desktop & Mobile**: logging a play with a player name that doesn't match an existing Member now auto-creates that Member, instead of silently losing the association. (v6.8.7, v2.2.4)
- **Desktop**: the Members tab wasn't refreshing after a play auto-created a new member — the member existed in the database but didn't appear until something else triggered a refresh. Also, the "Game" field when logging a play was accidentally locked to selection-only (no typing). Both fixed. (v6.8.8)

## Backup & restore

- **Desktop**: can now import a JSON backup (from Mobile, or Desktop's own "Export for Mobile") directly, merging in new members/plays/loans without needing the old full-database ZIP format. (v6.8.8)
- **Web**: added backup export/import entirely — previously Web had no backup feature of any kind. Uses the same JSON schema as Desktop and Mobile, so backup files are interchangeable across all three platforms. (v6.9.0)

## Dates & formatting

- All three platforms now display dates in US format (MM/DD/YYYY) with no time-of-day shown, instead of raw ISO timestamps. Sorting still works correctly against the underlying date value, not the reformatted text. (v6.8.8/v6.9.0, v2.2.8)
- The ambiguous 3D-insert package icon (📦) in Desktop's table view was replaced with a text label and checkmark. (v6.8.6)

## Accessibility

A full accessibility pass across all three platforms (v6.9.0, v2.2.8):

- **Web**: BGG search results (Add Game, Log Play) are now keyboard-operable, not mouse-only. Added missing form-label associations and `aria-label`s across several filter and modal forms. Fixed a color-contrast failure on the Dashboard's "winner" text. Added missing page-heading landmarks.
- **Mobile**: the bottom tab bar, collection/comparison chips, and all filter/checkbox controls now properly announce their role and state to screen readers — previously inconsistent across the app. Added labels to about 8 icon-only buttons that had none, and enlarged several undersized touch targets.
- **Desktop**: fixed a color-contrast failure and undersized font on the Games card view's A-Z jump bar. The favorite-star toggle is now keyboard-focusable and operable via Return/Space. Added Menu-key/Shift+F10 keyboard equivalents for every right-click context menu, and Return-key equivalents for Members' and History's double-click actions.
- **Known gap**: Desktop's card view (as opposed to table view) is still mouse-only for game-card interactions — a larger rework than this pass covered. Keyboard users should prefer Table view, which has full keyboard support.

## Store distribution (Mobile)

- Added CI workflows to build a signed Android App Bundle for Google Play and a signed iOS build for the App Store, in addition to the existing sideload APK. A `store-v*` git tag now triggers both together.
- Added store listing content (descriptions, keywords, Data Safety / App Privacy answers) and a hosted privacy policy required by both stores.

## Also in this window

- Fixed all 14 pre-existing TypeScript errors on Mobile (type-safety cleanup, no user-facing behavior change). (v2.2.0)
