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
- Costs table and "待讨论" list are plain HTML sections.
- The sketch map is drawn by the map IIFE from lon/lat points.
- Colors are CSS tokens on `:root` with dark-mode overrides; don't hard-code colors.

## Rules
- The repo is public: never put booking/confirmation codes, passport numbers, phone numbers, or payment info on the page.
- Times are local time at that place; Egypt is UTC+2, UAE is UTC+4.
- Keep the page working on phones (narrow width) and in both light and dark mode.
- Don't remove someone else's content without saying so in the commit message.
