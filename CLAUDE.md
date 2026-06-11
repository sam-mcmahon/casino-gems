# PRISMFALL — Claude Instructions

## MANDATORY: Version & Changelog Update on Every PR

**Before creating any PR, you MUST:**

1. Increment the version number in `index.html`
2. Add a new entry to the changelog in `index.html`

### Version numbering
- Minor fixes/tweaks → bump patch: `v1.5` → `v1.5.1`
- New features or meaningful gameplay changes → bump minor: `v1.5` → `v1.6`
- Major overhauls → bump major: `v1.x` → `v2.0`

### Where to update (two places, keep in sync)

**1. The `<summary>` tag** (shows version at a glance):
```html
<summary>v1.0 · PRISMFALL — Gem Cascade Casino</summary>
```

**2. The `#changelog` div** (prepend a new line at the top):
```html
<b>v1.1</b> — Short description of what changed in this PR<br>
<b>v1.0</b> — Previous entry...
```

Both are inside the `<details id="version-footer">` near the bottom of `index.html`.

## Current version: v1.4

## Architecture
- Single file: `index.html` — all CSS, JS, and HTML inline, no build step
- No external dependencies except Google Fonts (Orbitron + Rajdhani)
- Deployed via GitHub Pages from `main` branch
- Live at: https://sam-mcmahon.github.io/casino-gems
- Save key: `prismfall_v1` in localStorage

## Key constants (top of `<script>`)
- `COLS = 6`, `ROWS = 5` — scatter-pays grid, no paylines
- `SYMBOLS` — 10 paying gems; `pays` = [8-9, 10-11, 12+] win tiers × bet
- `SPECIALS` — 🌈 scatter, ⚡ charged gem, 🪙 gold nugget
- `BASE_SCATTER_W / BASE_CHARGE_W / BASE_COIN_W` — special-symbol weights (tune feature frequency here)
- `CHARGE_VALUES` — charged-gem multiplier table (×2–×500, weighted)
- `HW_VALUES` — Hold & Win coin values + MINI/MINOR/MAJOR jackpot coins
- `JP_SEED` — jackpot reseed values
- `FORGE_CAP = 150` — shattered gems needed to smelt a boon

## Game mechanics
- **Engine**: 8+ matching gems anywhere pays → winners shatter → tumble/cascade refills → repeat until no win
- **⚡ Charged Gems** survive tumbles; on a winning sequence all visible values sum and multiply the total win
- **Free spins** (4+ 🌈): charged-gem values accumulate into a persistent multiplier for the whole bonus; 3+ retriggers +5
- **Lightning Hold & Win** (6+ 🪙): lock-and-respin, 3 respins reset on landing, full 30-cell grid wins the GRAND
- **4 progressive jackpots** grow with wagers (Mini/Minor/Major/Grand)
- **Gem Forge**: shattered gems fill a meter; full meter = pick 1 of 3 boons (charged spins, free spins, Hold & Win, Gem Mine, Crystal Wheel, Gem Cutter, Coin Vault)
- **Mini-games**: Gem Mine (push-your-luck), Crystal Wheel (two-tier SVG wheel), Gem Cutter (timing skill)
- **Bonus Buy** (100×/200×/120× bet), **Ante Bet** (×1.25 cost, +50% scatter/nugget odds)
- **Gem Bank**: free token reloads via the Gems HUD card (placeholder for future monetization)
- **Engagement rule**: nothing auto-spins except the AUTO button — free spins and Hold & Win respins are player-triggered
- **Meta**: XP levels with rewards, 27 achievements, daily wheel (20h cooldown), session stats, spin history
- **Takeover events**: `SKINS` registry with `event` config — 🧟 Zombie Outbreak (winning cluster of 10+ 🟢 emerald) and 💪 Broforce Raid (10+ 🔺 ruby) take over the game for 10 spins (`state.modeSpins`): full reskin (CSS vars on `body.zombie`/`body.bro`, Nosifer/Creepster vs Press Start 2P fonts, neon crypt vs day-sky jungle, all 13 symbols via `skinE`/`skinName`, win tiers, particle colors) plus different winning — all wins ×2, outbreak boosts reanimation to 25%, raid adds per-spin strafing runs. Not user-toggleable; ends with "realm restores" interstitial
- **Revive mechanic**: in a takeover mode, a losing base-game spin has a `SKINS[skin].revive.chance` (8–10%) of being reanimated — lightning/airstrike flash (`#flash`), then `forceCluster()` grafts the most common gem to a paying 8-cluster and tumbles rerun
- All audio is synthesized via WebAudio — no sound files. All art is emoji/CSS/SVG/Canvas — no image files.

## Testing
Playwright headless smoke test pattern: load `file://.../index.html`, set
`state.turbo = true; state.sound = false`, call `doSpin()` in a loop, dismiss
`#mg-continue` / `#bigwin-overlay` between spins, assert no `pageerror`.
