# Navimoe — Agent Guidance

> **Project**: Navimoe — C.A.T.S. Buddy (desktop web version)  
> **Type**: Static HTML/jQuery single-page app  
> **Last Updated**: 2026-05-21

---

## Quick Reference

| Item | Value |
|------|-------|
| Entry Point | `index.html` |
| Main Logic | `cats.js` |
| Game Data | `data.js` |
| Styles | `style.css` |
| Build Step | None — static files |
| Tests | None |

---

## Architecture

Navimoe is a **static jQuery-based SPA** with no backend and no build step.

### Script Load Order

```html
<script src="jquery-3.6.1.min.js"></script>
<script src="common.js"></script>   <!-- logger -->
<script src="data.js"></script>     <!-- constants, createItem, mapToLevelBySip -->
<script src="cats.js"></script>     <!-- jQuery UI logic, TableBuilder, item classes -->
```

### Layout

- **Two-pane desktop layout**: Left pane = Car Builder + Level Mapper + Settings. Right pane = Lineup filters + item grid.
- All interaction is click-based on `<td>` elements inside filter tables.
- The `#lineup-table` is populated dynamically by jQuery.

---

## Code Conventions

- **jQuery-heavy**: Uses `$` for DOM manipulation, event binding, and AJAX (if any).
- **ES5 style**: Uses `var` and `function` declarations.
- **Global constants**: All game data constants are prefixed with `G_` (e.g., `G_BODY`, `G_R6`).

---

## Common Tasks

### Adding a New Filter

1. Add filter HTML in `index.html` inside `#filters` (follow existing `<table>` structure).
2. Add click handler in `cats.js` (search for filter `click` bindings).
3. Add filtering logic in the item render pipeline.

### Adding a New Item

1. Add item data to `data.js` (inside the item pool).
2. Add the item image to `images/`.
3. Verify it appears in Lineup with correct filters.

### Changing Styling

- `style.css` is small (~160 lines). Most styling is inline or table-based.
- The layout relies on `.left-pane` (fixed narrow width) and `.right-pane` (flex remaining).

---

## Image Assets

All item images are in `images/` as PNGs. These are shared with MiniNavimoe.

If you add new images here, run the sync script from MiniNavimoe so both projects stay in sync:

```bash
# Run from MiniNavimoe directory
./scripts/sync-images-from-navimoe.sh
```

---

## Deployment Context

Navimoe is a **static website** with no server-side component. It can be served by any static file server (nginx, Python `http.server`, GitHub Pages, etc.).

There is no Docker container or `docker-compose.yml` in this directory. If deploying, copy the folder contents to any web root.

---

## Related Projects

- `../MiniNavimoe/` — Telegram MiniApp version (vanilla JS, mobile-first, forked from this project)
- `../bsnavimoe-react/` — Full React + FastAPI + Supabase version (separate modern rewrite)

---

## Fork History

- **Upstream**: `https://github.com/SAK-20744/Navimoe.git`
- **This fork**: `https://github.com/invidtiv/Navimoe.git`
