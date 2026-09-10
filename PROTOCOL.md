# TOAA Desk Protocol

Repo is **public**. No secrets, tokens, PATs, CLOB keys, bank logins, custody docs, SAM/EIN dumps.

OLE / SBIR / entity filings live in private `Dmgedgoodz/Orbitalreclaim-LLC.` only.

## Same-page loop
1. Operator or Grok reads `DESK/_last.md` then `INBOX/`.
2. Work happens. Results commit to this repo or the LLC repo as scoped.
3. Overwrite `DESK/_last.md` with status, locks, next three moves, paths touched.
4. Move finished inbox notes to `INBOX/done/` or delete.

## Session opener (paste this)
```
Sync TOAA. Read DESK/_last.md and INBOX. Execute.
```

## Paths
| Path | Owner |
|---|---|
| `DESK/_last.md` | Operational brief. Overwrite in place. |
| `INBOX/*.md` | New asks. First 20 lines = the task. |
| `Chronicle/_last.md` | Narrative hook only. Do not use as ops brief. |
| `AEGIS-FLOOR/` | Risk lock + build prompt. |
| `sources/` | Pointers, not mirrors. |
