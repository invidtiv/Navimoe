# Navimoe — C.A.T.S. Buddy

A desktop web companion for **C.A.T.S.: Crash Arena Turbo Stars**. Browse game items, build cars, and map level stats.

> **Note**: Navimoe is the original static HTML/jQuery version. For the Telegram MiniApp, see `../MiniNavimoe/`. For the full React + Supabase version, see `../bsnavimoe-react/`.

## What It Does

Navimoe provides three core features for C.A.T.S. players:

1. **Lineup** — Browse the full catalog of C.A.T.S. items with rich filters (view, sponsor, rarity, power, class, sort). Items are displayed in a grid table with images and stats.
2. **Car Builder** — Assemble cars by clicking items in Lineup. View total HP/ATK and item bonuses. Build multiple cars simultaneously.
3. **Level Mapper** — Calculate stats at any level for any item using known stat increment patterns (R1–R6). Click any item image in Lineup to auto-fill.

## Tech Stack

- **Frontend**: HTML5 + jQuery 3.6.1
- **Styling**: Custom CSS
- **Data**: Static JSON-like JS modules (`data.js`, `cats.js`)
- **No build step** — Open `index.html` directly or serve statically
- **No backend** — All data is client-side

## Project Structure

```
Navimoe/
├── index.html              # Two-pane desktop layout
├── style.css               # Desktop-specific styles (~160 lines)
├── cats.js                 # UI logic and game data classes (~1027 lines)
├── data.js                 # Game data constants and helpers (~932 lines)
├── common.js               # Shared logger utility
├── jquery-3.6.1.min.js     # jQuery dependency
└── images/                 # Item and sponsor PNGs (~170 images)
```

## Running Locally

No build step required. Open `index.html` directly in a browser, or serve with any static server:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080`.

## Data Model

Game data lives in three files:

- **`data.js`** — Constants (rarities, categories, sponsors, classes, bonuses, stat increment patterns) and helper functions (`createItem`, `mapToLevelBySip`, `estimateCosts`).
- **`cats.js`** — `TableBuilder`, `LineupItem`, `CarBuilderItem`, `LevelMapperItem` classes, and jQuery-based UI rendering.
- **`parts.json`** — Not present in Navimoe (MiniNavimoe uses it); all item data is embedded in `data.js`.

## Filters

The Lineup supports these filter dimensions:

| Filter | Options |
|--------|---------|
| View | All, All HP, All ATK, Bodies, Weapons, Wheels, Gadgets |
| Sponsor | All, Mecha Corp, Naturalis Inc, Gluttony Ltd, Sporty LLC, None |
| Rarity | All, R6, R5, R4, R3, R2, R1 |
| Power | All, -15, -10, -5, 0, +5, +15, +20, +25, +30, +35, +40 |
| Class | All, Melee, Ranged, Auto-Aim, Minion, Special, None |
| Sort By | Default, HP, ATK |

## Level Mapper Patterns

| Pattern | Description |
|---------|-------------|
| R6 | Standard R6 increment |
| R6 Legacy (Naturalis) | Legacy Naturalis R6 pattern |
| R5 | R5 increment |
| R4 | R4 increment |
| R3 | R3 increment |
| R2 | R2 increment |
| R1 | R1 increment |

## Relationship to MiniNavimoe

Navimoe is the **upstream source** for MiniNavimoe:

- `data.js` and `cats.js` core logic were ported from Navimoe to MiniNavimoe.
- Item images are shared; MiniNavimoe syncs from Navimoe via `../MiniNavimoe/scripts/sync-images-from-navimoe.sh`.
- Navimoe uses jQuery and a two-pane desktop layout.
- MiniNavimoe uses vanilla JS and a mobile tab layout with Telegram WebApp integration.

## Fork History

- **Upstream**: https://github.com/SAK-20744/Navimoe.git
- **Fork**: https://github.com/invidtiv/Navimoe.git

## Credits

- Data by SAK26
- Unofficial companion tool — not affiliated with ZeptoLab
