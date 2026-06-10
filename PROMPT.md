# The One-Shot Prompt

This repo was built in a single session from the prompt below.

---

**Build "PRISMFALL — Gem Cascade Casino"** in a new public repo `casino-gems`: a
single-file, no-build, no-dependency `index.html` browser slot that is 5× deeper
than Lucky Paws Casino ([casino-cats](https://github.com/sam-mcmahon/casino-cats))
and feels like a bleeding-edge 2026 real-money slot. Same constraints as
casino-cats (one file, emoji/CSS/Canvas art only, localStorage persistence,
GitHub Pages ready) but a completely new engine:

**Core engine — modern, not paylines:**
1. **6×5 grid with scatter-pays**: 8+ matching gems *anywhere* pays — no paylines.
2. **Cascade/tumble mechanic**: winning gems shatter with particle bursts, gems
   above fall, new ones drop in, chains continue until no win — with a tumble
   counter and escalating sound pitch.
3. **Charged Gems (⚡)**: multiplier orbs ×2–×500 that land randomly; at the end
   of a winning tumble sequence all visible orbs sum and multiply the total.
4. **Free Spins (4+ 🌈 Prism Scatters)**: every applied orb adds to a
   *persistent accumulating multiplier* for the rest of the bonus.
5. **Lightning Hold & Win (6+ 🪙)**: coins lock, 3 respins, every new coin resets
   the count, fill all 30 cells for the GRAND. Coins carry values plus
   MINI/MINOR/MAJOR jackpot coins.
6. **4-tier progressive jackpots** (Mini/Minor/Major/Grand) growing with every bet.

**Depth layer:**
7. **The Gem Forge**: every shattered gem feeds a forge meter; a full forge
   offers a pick-1-of-3 **Boon** (super-charged spins, instant bonus, coin vaults…).
8. **Mini-games**: Gem Mine (push-your-luck tile picks with cave-ins), Crystal
   Wheel (two-tier wheel with upgrade to a premium inner wheel), Gem Cutter
   (timing-bar skill cut for multipliers), Daily Bonus Wheel.
9. **Bonus Buy menu** (100×/200× bet) and **Ante Bet** toggle (+25% bet, boosted
   scatter odds).
10. **Meta-progression**: XP & player levels with rewards, 24 achievements,
    lifetime stats panel, spin history.

**Presentation:**
11. **WebAudio synthesized sound engine** — no audio files: spin whoosh,
    crystalline shatter chimes, anticipation risers when 3 scatters land,
    big-win fanfares.
12. **Big Win ladder** (BIG → MEGA → EPIC → LEGENDARY) with count-up totals,
    screen shake, coin showers; scatter anticipation slow-downs;
    aurora/glassmorphism dark-prismatic art direction (Orbitron-style display
    font, cyan/magenta/gold on obsidian).
13. Turbo mode, autoplay with stop conditions, keyboard + swipe controls,
    mobile-first responsive, haptics.

Ship with `CLAUDE.md` (same versioning rules as casino-cats), `README.md`, and a
version footer starting at v1.0.
