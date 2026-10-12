# SQLeLite

Lightweight Oracle SQL Client — a modern replacement for SQL Navigator.

> Developed by **NhảmStudio**

---

## Features

### SQL Editor
- Multi-tab editor, line numbers, syntax highlighting (keywords, built-ins, strings, comments, binds)
  that stays fast on 10k+ line packages (only the visible region is painted)
- **F8 / Ctrl+Enter** runs the statement at the cursor (or every statement in the selection);
  a blank line ends the statement, like Toad/SQL Developer (toggle in *Run* menu)
- **F9 / F5** runs the whole script. Statements end at `;` or a `/` line; PL/SQL blocks
  (`DECLARE`/`BEGIN`, `CREATE PROCEDURE/FUNCTION/PACKAGE/TRIGGER/TYPE`) are detected even without `/`
- SQL*Plus commands in scripts: `DESC`, `EXEC`, `PROMPT`, `SET SERVEROUTPUT ON|OFF`, `SHOW ERRORS`
  (other `SET`/`SPOOL`/`COLUMN`… lines are skipped instead of breaking the script)
- Queries run in the background: the window never freezes and **Stop (Ctrl+Break)** really cancels
- Bind variables (`:name`) prompt for values (remembered per session)
- DBMS_OUTPUT shown automatically after each statement
- Oracle errors link to the exact position / line in the editor
- Autocomplete (Ctrl+Space or while typing): objects, keywords, `alias.` → columns,
  `schema.` → objects, `package.` → subprograms; keyboard navigation
- **Go to definition**: F3 / F12 / Ctrl+Click on `table`, `pkg.proc`, `schema.pkg.proc`
- Format SQL (Ctrl+R, selection or all), Find/Replace with regex (Ctrl+F), toggle comment (Ctrl+/),
  upper/lower case, duplicate line, indent/unindent, Ctrl+Wheel zoom

- **Code templates** (Ctrl+J): type `sel`, `ins`, `upd`, `decl`, `forc`, `proc`, `pkg`, `trg`… then Ctrl+J;
  Ctrl+J on an unknown word lists templates. Add your own in `templates.json` (*Tools › Edit Code Templates*)
- **Explain Plan** (Ctrl+E): plan tree in the grid + DBMS_XPLAN text in Output (runs on a separate
  session and is rolled back, so your transaction is untouched)
- **SQL History** (Ctrl+Shift+H): every executed statement with time, connection, status and elapsed;
  search, insert, open in new tab or run again

### Session restore
- All tabs (including unsaved text and uncompiled PL/SQL edits), cursor position, window layout
  and bind values are autosaved every 15 s to `workspace.json` and restored on the next start —
  also after a crash

### Stored program editor (packages, procedures, functions, triggers, types)
- Source loaded from `ALL_SOURCE`, so editor lines match compiler error lines
- Spec / Body tabs, **Outline** of procedures/functions/cursors/types — click to jump
- Compile (F9 / Ctrl+S) on a separate session (never commits your open transaction);
  error list with click-to-line, error lines highlighted
- An object is never opened twice; reload from DB

### Schema Browser
- Loads in the background, one query per schema; your schema first and expanded
- Tables, Views, Materialized Views, Packages, Procedures, Functions, Types, Triggers, Sequences, Synonyms
- Filter box, invalid objects in red with counts
- Packages expand to their public subprograms — double-click opens the body at that subprogram
- Tables expand to columns, indexes, constraints, triggers
- Context menu: Query data, Describe, Generate SELECT, Edit source, Create Script (DDL), Compile,
  Insert name, Copy (qualified) name

### Result Grid
- Each editor tab keeps its own results; a script produces one result tab per query
- Rows load page by page while scrolling; **Fetch All** continues the same cursor (no re-execution)
- Click header to sort (numeric/date aware, NULLs last), quick filter, row numbers, auto column width
- Cell value bar, cell viewer (double-click), **Record view** (Enter)
- Copy cell / rows / rows with header / column / IN-list / INSERT statements
- Export to XLSX (typed numbers & dates), CSV, INSERT script
- CLOB/BLOB shown as text/hex, NUMBER shown exactly (no float rounding)
- **Edit data** (✎ Edit on a single-table SELECT): the query is re-run with ROWID; F2 / double-click
  edits a cell (Tab moves on), *Edit in window* for long text, *Set NULL*, Insert adds a row, Delete
  marks rows; **Apply** writes everything in one savepoint (all or nothing), **Revert** discards.
  Numbers and dates are validated (`YYYY-MM-DD [HH:MI:SS]` or `DD/MM/YYYY`). Changes follow the
  Auto Commit setting

### Find object & dependencies
- *Tools › Find Object* (Ctrl+Shift+O): search every schema you can see (`*` wildcard, type filter);
  open, DDL, describe, dependencies
- Schema browser / Find Object: **Dependencies** shows what an object uses and what uses it

### Multiple connections
- *File › New Window* (Ctrl+Shift+N) opens another SQLeLite window with its own connection.
  Each window has its own workspace (`workspace.json`, `workspace-2.json`, …) and is restored separately

### Transactions & connection
- Manual COMMIT/ROLLBACK by default (Auto Commit toggle on the toolbar), uncommitted-transaction
  indicator, prompt on exit/disconnect
- Saved connections, reconnect on startup. Passwords are protected with **Windows DPAPI** (tied to
  your Windows account); old `key.key` passwords are migrated automatically
- Leave *Host* empty to use a TNS alias or full connect string in *Service Name*
- Oracle < 12.1: set `"thick_mode": true` (and `oracle_client_dir`) in `settings.json`

---

## Files next to the exe
| File | Purpose |
|---|---|
| `connections.json` | saved connections (DPAPI-protected passwords; `key.key` only needed for old entries) |
| `settings.json` | options (fetch size, autocommit, font size, thick mode…) |
| `workspace.json` (+ `.bak`), `workspace-N.json` | autosaved tabs/session per window |
| `history.json` | SQL history (last 3000 statements) |
| `templates.json` | your code templates (created by *Edit Code Templates*) |
| `sqlelite.log` | internal errors |

## Build
```
python -m PyInstaller SQLeLite.spec --noconfirm
```

## Tests (no database needed)
```
python tests/test_sqltext.py
python tests/test_config.py
python tests/smoke_gui.py
python tests/smoke_exec.py
```

## Requirements
- Windows x64
- Network access to the Oracle database (Thin mode, no client needed for Oracle 12.1+)

---

## License

Copyright &copy; 2026 SQLeLite. All rights reserved.
