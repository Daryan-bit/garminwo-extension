# Changelog — GarminWO

All notable changes to this project will be documented in this file.

---

## [1.4.24] — 2026-04-22
### Changed
- Removed "Report a Bug" button — replaced by a simple contact email line in the modal footer

## [1.4.23] — 2026-04-22
### Added
- Switch engine button (⚡ Retry with Claude/Gemini) appears when quota is exceeded — automatically switches to the other engine and retries
- Dynamic analysis message: "🔍 Analyse par Gemini en cours..." or "🔍 Analyse par Claude en cours..." depending on selected engine
- Bug report button (🐛) opening a contact page on GitHub Pages with pre-filled fields

## [1.4.22] — 2026-04-22
### Added
- Dynamic loading message shows the AI engine name (Gemini or Claude) instead of generic text
- Bug report button (🐛) in modal header — opens contact page with version, engine and error pre-filled

## [1.4.21] — 2026-04-22
### Added
- Gemini fallback: automatically switches to `gemini-2.0-flash` if `gemini-2.5-flash` returns 429/503
- Clear quota error message with retry delay extracted from API response
### Fixed
- `getApiKey()` protected with try/catch against "Extension context invalidated" error after extension reload

## [1.4.20] — 2026-04-22
### Fixed
- Duplicate workout names now handled correctly — cache stores a list of IDs per name instead of a single ID, so selecting multiple workouts with the same name no longer causes incorrect count in the delete bar

## [1.4.19] — 2026-04-22
### Fixed
- Guard against `undefined` values being added to the selection Set when checking a row with no cached ID
- Cleanup of `undefined/null` entries in the Set before counting selected workouts

## [1.4.18] — 2026-04-22
### Fixed
- Post-import redirect now uses `?workoutType=running` parameter required by Garmin Connect v5.24
- Cache is reloaded after import to retrieve the freshly created workout ID

## [1.4.17] — 2026-04-22
### Fixed
- Replaced `MutationObserver` on `document.body` with a simple `setInterval` polling (every 2s) to detect new rows — eliminates infinite loop that froze Garmin Connect when checking a checkbox

## [1.4.16] — 2026-04-22
### Fixed
- `MutationObserver` now disconnects before and reconnects after `renderCheckboxes()` to prevent re-entrancy loops

## [1.4.15] — 2026-04-22
### Fixed
- `renderCheckboxes()` made synchronous again — `loadWorkoutIds()` called only once before the observer starts

## [1.4.14] — 2026-04-22
### Fixed
- `loadWorkoutIds()` loading flag prevents multiple simultaneous calls
- Post-import redirect reloads cache before navigating to the new workout page

## [1.4.13] — 2026-04-22
### Fixed
- CSRF token now read from `<meta name="csrf-token">` tag instead of cookies (changed in Garmin Connect v5.24)
- Applied to `loadWorkoutIds`, `importWorkout` and `confirmAndDelete`

## [1.4.12] — 2026-04-22
### Fixed
- `loadWorkoutIds()` uses relative URL `/gc-api/...` to avoid CORS restrictions in content script

## [1.4.11] — 2026-04-22
### Fixed
- Workout IDs now fetched via `GWO_FETCH_WORKOUT_IDS` message to background service worker to bypass content script CORS restrictions

## [1.4.10] — 2026-04-22
### Fixed
- Compatibility with Garmin Connect v5.24 update:
  - All URLs updated from `/modern/workouts` to `/app/workouts`
  - Checkbox selectors updated to use `className.includes()` instead of CSS attribute selectors (incompatible with special characters in class names)
  - Link selector updated from `a[href*="/workout/"]` to `[class*="workoutName"] button/a` (Garmin replaced `<a>` tags with `<button>` elements)
  - Post-import redirect updated to `/app/workout/{id}?workoutType=running`

---

## [1.4.9] — 2026-04-20
### Fixed
- Retry button now correctly re-sends selected text to AI (was falling back to image analysis)
- Added `currentPendingText` global variable to preserve text across retry attempts

## [1.4.8] — 2026-04-20
### Fixed
- Workout ID fetch via intercepted fetch — replaced by background API call approach

## [1.4.7] — 2026-04-20
### Fixed
- Redirect after import falls back to `/app/workouts` list if no workout ID available
- Link selector made more robust for varying Garmin DOM structures

## [1.4.6] — 2026-04-20
### Fixed
- Checkbox row selector uses `Array.from().filter()` instead of `querySelectorAll('[class*=...]')` to handle special characters (`+`) in Garmin CSS class names

## [1.4.5] — 2026-04-19
### Fixed
- Post-import redirect polling: checks URL availability every 500ms instead of fixed delay (max 15s fallback)

## [1.4.4] — 2026-04-19
### Fixed
- Post-import redirect URL updated to `/app/workout/{id}` (Garmin Connect URL structure change)
- Redirect delay increased from 2s to 6s to allow Garmin server to make the workout available

## [1.4.3] — 2026-04-18
### Changed
- Chrome Web Store submission: added justifications for `contextMenus`, `tabs` and `*://*/*` host permissions
- Host permissions limited to specific domains as alternative (reverted to `*://*/*` for flexibility)

## [1.4.2] — 2026-04-17
### Fixed
- `t()` i18n helper now uses a local cache and built-in EN fallback dictionary — prevents raw key display when service worker is asleep after extended navigation

## [1.4.1] — 2026-04-16
### Fixed
- Checkbox observer reset on page change — checkboxes now re-inject correctly when navigating between workout list pages

## [1.4.0] — 2026-04-15
### Fixed
- `try/catch` added around `chrome.runtime.sendMessage()` calls in `checkPendingImage()` and `checkPendingText()` — prevents uncaught errors when service worker is inactive

---

## [1.3.9] — 2026-04-14
### Fixed
- `injectCheckboxes()` waits for table rows to be present in DOM before injecting (retry every 300ms, max 20 attempts)

## [1.3.8] — 2026-04-14
### Fixed
- Checkbox row selector changed to `[class*="tableRow"]` to handle special characters in Garmin CSS class names

## [1.3.7] — 2026-04-14
### Added
- **Bulk delete** — checkboxes injected into the native Garmin Connect workout list
- "Select all" checkbox in table header
- Floating delete bar with count, Cancel and Delete buttons
- Confirmation dialog before deletion
- Rows removed from DOM immediately after successful deletion

## [1.3.6] — 2026-04-13
### Fixed
- Added missing `tabs` permission in `manifest.json` — was causing silent failure of `chrome.tabs.query()` and `chrome.tabs.update()` in background service worker

## [1.3.5] — 2026-04-13
### Changed
- After successful import, redirects directly to the created workout page instead of reloading the list

## [1.3.4] — 2026-04-13
### Fixed
- Retry button correctly re-sends text to AI after a failed text analysis
- `currentPendingText` preserved for retry

## [1.3.3] — 2026-04-12
### Changed
- Version alignment

## [1.3.2] — 2026-04-12
### Added
- **Retry button** — appears in the error block for temporary API errors (overload, timeout)
- Retry is context-aware: re-runs image analysis, text analysis, or import depending on current state

## [1.3.1] — 2026-04-12
### Added
- **Right-click on selected text** — select any workout plan text on any web page → right-click → "Send to GarminWO" → AI analyses and imports directly
- Text analysis via Gemini (`analyzeTextWithGemini`) and Claude (`analyzeTextWithClaude`)
- `ANALYZE_TEXT` message handler in background service worker

## [1.3.0] — 2026-04-11
### Added
- **Right-click on image** — right-click any image on any web page → "Send to GarminWO"
- Image fetched and stored in `chrome.storage.local` as pending
- If a Garmin Connect Workouts tab is already open: activates it and opens the modal automatically
- Otherwise: opens a new Garmin Connect tab (content.js detects the pending image on load)
- `contextMenus` and `tabs` permissions added to manifest

---

## [1.2.x] — 2026-03-xx
### Added
- Google Gemini engine support (free, 1500 req/day)
- Engine selector tabs in popup (Gemini / Claude)
- JSON file import (no AI call required)
- Help button (?) in modal — opens language-specific PDF guide
- 6 language support: FR, EN, ES, DE, IT, RU
- Full i18n audit and corrections across all locales
- PDF help guides for all 6 languages

---

## [1.1.0] — 2026-02-xx
### Added
- Initial release
- Import running workouts into Garmin Connect from a photo or screenshot
- AI analysis via Anthropic Claude
- Popup configuration for API key
- Automatic injection of import button on Garmin Connect Workouts page
- Support for all native Garmin step types: warmup, interval, recovery, cooldown, repeat
- End conditions: distance, time, lap button
