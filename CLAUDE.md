# 开罗 · 达哈卜 2026 — notes for AI assistants

This repo is a 4-person trip page published with GitHub Pages:
https://rvme.github.io/egypt-trip-2026/
Several people (and their Claude / Codex) edit it, so follow these rules.

## Workflow
1. `git pull --rebase` before every edit, and push right after (small commits, clear message in Chinese or English).
2. Everything lives in one file: `index.html`. No build step. GitHub Pages redeploys about 1 minute after a push.
3. Open the page locally (or check the Pages URL after pushing) and confirm it still renders before you finish.
4. If a push is rejected, pull with rebase, resolve conflicts keeping both people's intent, then push again.

## Where things are in `index.html`
- `const DAYS = [...]` — the day-by-day plan. Each item: `t` (local time "HH:MM"), `tz` ("+02:00" Egypt, "+04:00" UAE), `what`, optional `note`, `place` (Google Maps search text → "导航" link), `tag` ("fly" | "book" | "warn"), `ev: true` for key moments the countdown should highlight.
- `const TODO = [...]` — checklist rows `[id, text, when]`. Ticks are stored per device (localStorage); keep ids stable.
- Costs table (`.cost`, one row per item, AED shown under the ¥ figure when the price was paid in AED) and "待讨论" list (only open questions) are plain HTML sections.
- Section ids, in page order (trip-use order: what to do / where to go / who to call): `plan` (每日行程; the inner `id="days"` div is filled by `renderDays`) → `todo-sec` (待办; inner `id="todo"`) → `stay` (住哪) → `transport` (交通, the decided plan; alternatives sit in one closed `<details>`) → `dahab` (达哈卜玩什么) → `food` (吃喝地图) → `info` (实用信息, incl. 应急电话 + 旅行保险) → `costs` (费用) → `qs` (待讨论, last, before the footer). A chip row under the header (`.qnav`) links to them in the same order, so keep ids and the chip list in sync when you add a section. Keep each fact once and cross-reference it (e.g. 「实用信息 → 旅行保险」) instead of repeating it.
- Place links: write `<a class="go" data-q="Maps search text" target="_blank" rel="noopener">导航</a>` and, for hotels, `<a class="go" data-bk="hotel name" ...>Booking</a>`. `fillLinks()` at the end of the script sets the `href` (via `Q()` / Booking search URL); don't hand-encode URLs.
- The sketch map is drawn by the map IIFE from lon/lat points.
- Colors are CSS tokens on `:root` with dark-mode overrides; don't hard-code colors.

## Rules
- The repo is public: never put booking/confirmation codes, passport numbers, payment info, or private individuals' phone numbers on the page. Public official/company hotlines (emergency numbers, embassy, Go Bus) are fine.
- Times are local time at that place; Egypt is UTC+2, UAE is UTC+4.
- Keep the page working on phones (narrow width) and in both light and dark mode.
- Don't remove someone else's content without saying so in the commit message.
