# About / Guide

**S&P Catalog {{version}}** — private catalog for works, cowriters, performers, releases, society income, payouts, and expenses. WordPress settings (My Catalog, About, Designer) are for setup. Users, Art / xAI, Royalty math, and Health live on My Catalog. Day-to-day work is **Works** (internal) and **App** (public catalog).

## Two interfaces

- **Works** (`/db/`) — login required. Catalog editors and admins. Hamburger: Works, Releases, People, Pay, Statements, Sessions, Art studio, Contracts, Expenses. All load on this page.
- **App** (`/app/`) — open to the public. Search and play the catalog. Log in from the menu. After login, the menu shows tools for that user class (Account for everyone; Sessions for the Sessions class; Works for editors).
- **Contributor** — public catalog + their credited works and statement.
- **Sessions** — that plus writing sessions (on the App).
- **Catalog editor / Administrator** — Works editor with every internal tool.
- Old extra pages (People, Payouts, Reports, …) redirect into Works or App. You can trash those pages later.

## First run

- Open **Publishing / Writing Catalog → My Catalog**.
- Enter publisher + IPI and writer + IPI. You need a writer and/or publisher account at a PRO (ASCAP, BMI, SESAC, PRS, or your region). The PRO link on that screen is editable.
- Set branding: company name, app name, welcome text, print footer, optional logo. The public app and lead sheets use these labels.
- Use **Full backup** before every plugin upload (plugin + SQLite). Keep **Last-good plugin zip** after Health looks good (plugin files only). Updates and SQLite migrate live on My Catalog.
- Add people, then add a work in Works. Empty list? Ingest `sample-catalog.csv`, then delete those demo rows.

## Database

- Live file: `{{db_path}}`
- PHP needs `pdo_sqlite`. Path is `uploads/songwriting-publishing/catalog.sqlite`.
- This plugin uses the `swp_` prefix. The older Songwriting Catalog uses `swc_`. Do not point both at the same Works page.
- Serial format (default `XXXX-XX`) is on My Catalog. Export a backup before rewrite.
- Ingest maps CSV / TSV / XLSX / SQLite columns onto catalog fields and can add a field.

## Where to work

- **My Catalog** — setup, branding, included tools, Art / xAI key, Royalty math, users, updates, database migrate, Full backup, last-good zip, SQLite/CSV export, ingest, serial format.
- **Works** — list + editor. Plain page with `[works]` (usually `/db/`). Tools in the hamburger, not separate pages. Do not put this in Elementor.
- **App** — public `[catalog]` at `/app/`. Login in the app menu.
- **Designer** — form layouts for Works, Released, Sessions (if Sessions is on). Column show/hide for society and people lists.
- **People** — aliases, hide-from-reports, person details, **Access class**. New users start as Contributor.
- **Public app** — `[catalog]`. Search (including lyrics), ratings, share, print. Login from the app menu.
- **Account** — signed-in writers see credited works and a statement on the App.
- **Sessions** — from the App menu for Sessions-class users; from the Works menu for editors.
- **Royalties** — society uploads, per person, per work, amounts paid. Totals rebuild when you upload or edit a statement, not when you save a work.
- **Art studio** — generate sleeves. Toggle in My Catalog. xAI key is on My Catalog → Art / xAI.
- **Health** — SQLite path, table counts, last AJAX error (nonce / db / js / network). On My Catalog.

## User roles

- **Administrator** — everything, including users.
- **Catalog editor** (`edit_song_catalog`) — Works, royalties, people. No theme or page editing.
- **Sessions** (`edit_song_sessions`) — Sessions tool only, if that tool is on.
- **Contributor** — default for new users and session invites. Full public catalog. Sessions only if invited. No Works editor.
- Public visitors use the app with no login. Share links use `?serial=0001-01`.
- Link a WordPress user on the person editor so they see their own statement from the app header.

## Royalty rules

- Only tracks with an **ISRC** count as released for royalty math.
- Writer money: **MLC + ASCAP**, plus CCLI even-split by CCLI#. DistroKid is not writer income.
- Performer and producer DistroKid cuts are **off** until you turn them on under Royalty math.
- Splits come from the **catalog** writer %, not names on society CSVs. Aliases on People merge spellings.
- Pages read stored rollups. Matching runs when a statement is uploaded or a report row is edited/deleted.

## Files and backups

- Album art, logos, and audio URLs point at the Media Library.
- **Full backup** — plugin + databases. Before every zip upload.
- **Last-good plugin zip** — plugin files only, saved as `songwriting-publishing-database-last-good.zip`.
- Deleting this plugin does not delete `catalog.sqlite` or media.

## Shortcodes

- `[works]` — Works editor (also `[works_editor]`)
- `[released]` — Released works
- `[catalog]` — public catalog / app (Log in in the header)
- `[sessions]` / `[journal]` / `[session]` — writing sessions (if that tool is on)
- `[people]` — people directory
- `[payouts]` `[people_quarterly]`
- `[royalties]` `[royalties_quarterly]` `[released_quarterly]` `[my_royalties]`
- `[reports]` — society statements
- `[expenses]` `[contracts]`
- `[art_studio]` — album art studio (if that tool is on)

## If it looks stuck

- Hard-refresh after every upload. Version is {{version}}.
- Keep Works on a plain page. Do not put the editor in Elementor.
- Exclude `/db/`, `/wp-admin/admin-ajax.php`, and this plugin’s `assets/` folder from cache and Combine JS.
- Health shows engine, table counts, and the last AJAX error. Read that before changing the editor.
- If an update fails: upload last-good, or restore Full backup’s `plugin/` folder and copy `databases/` back to uploads.
