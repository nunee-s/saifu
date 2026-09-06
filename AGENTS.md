# Saifu — project memory

Single-file PWA at repo root (`index.html`, vanilla JS IIFE, no build step).
Deploy = commit + push to `main` → GitHub Pages: https://nunee-s.github.io/saifu/
Dev server: `python3 -m http.server 8080` (phone on same Wi-Fi: http://192.168.1.50:8080)

## Data model
- localStorage key `saifu.books.v1` (legacy `warikan.crew.v1` migrated in `load()`)
- `state = {books:[{id,name,currency,members:[{id,name}],expenses:[],settlements:[]}], activeBookId}`
- `expense = {id,description,date,payerId,total,mode:'even'|'amount',shares:[{memberId,amount}],items:[{label,amount,people:[ids]}]}`
- Old saved mode `'items'` is read back as `'amount'` (shared items kept in `form.items`)

## Expense entry (2 tabs)
- **Split evenly**: bill total ÷ ticked people; rounding remainder goes to the last person so shares sum exactly to the total
- **Per person**: per-person amounts + optional shared items (price split equally between ticked people, added on top of their share)
- "Who pays who" preview (`settlePreview`) and `formTotal` update live on every input; `saveExpense` uses the same `currentShares()` math as the preview — keep them in sync

## Gotchas
- Service worker `sw-v6.js` caches, but navigation is network-first so page updates propagate automatically; only bump the version if static assets change
- `source_code/` and `.DS_Store` are untracked artifacts — don't commit
- `window.saifu={transfers}` is the only public API; loop test stubs `document`/`localStorage` and patches that line to reach internals
- Commit style: `feat(saifu): ...` / `fix(saifu): ...`
