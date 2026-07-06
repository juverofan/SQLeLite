# SQLeLite

Lightweight Oracle SQL Client — a modern replacement for SQL Navigator.

> Developed by **NhảmStudio**

---

## Features

### SQL Editor
- Multi-tab editor with syntax highlighting (keywords, strings, numbers, comments)
- Run current statement (F8) or entire script (F9)
- SQL formatting with configurable clause indentation
- Find & Replace dialog
- Open/Save `.sql` files

### Schema Browser
- Browse schemas: Tables, Views, Packages, Procedures, Functions, Sequences, Synonyms, Triggers
- Right-click context menu: **Open** (opens SELECT\* for Table/View, DDL for others), **Create Script (DDL)**, **Desc Table**, **Copy Name**
- Real-time object status: valid objects in green, invalid in red
- Expand tables to view columns, indexes, constraints, and triggers inline

### Package Editor
- Open packages in a dedicated editor with **Spec** and **Body** sub-tabs
- Compile Spec, Body, or All directly to the database
- Ctrl+S to compile package to DB

### Result Grid
- Tabular query results with column headers
- **Fetch All** button to retrieve full result set (beyond 250-row preview)
- Inline cell editing — double-click to edit, yellow highlight for modified cells, **Save Changes** to generate UPDATE statements
- Execution history — click previous SQL to re-run
- Export results to XLSX / CSV / HTML

### Connection Management
- Connect to Oracle via host/port/service name
- Saved connections with quick-select dropdown
- Reconnect on startup — detects previous session and offers one-click reconnect
- Commit / Rollback toolbar buttons
- Connection status indicator

### Other Tools
- Extract DDL by schema, object type, and name
- Schema tree auto-refresh on connect

---

## Requirements

- Windows x64
- Oracle Instant Client (or Oracle DB with network access)
- No installation required — just run the `.exe`

---

## License

Copyright &copy; 2026 SQLeLite. All rights reserved.
