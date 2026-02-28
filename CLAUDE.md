# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Tetonor is a single-file browser puzzle game (`tetonor.html`). All HTML, CSS, and JS live in that one file. `www/index.html` is a copy of it — the web root that Capacitor serves for the Android build.

**When editing the game, edit `tetonor.html`, then copy it to `www/index.html`:**
```bash
cp tetonor.html www/index.html
```

## Android / Capacitor Build

Requires Node.js and Android Studio (with Android SDK) installed.

```bash
# First-time setup (after Node.js is installed)
npm install
npx cap add android

# After any change to www/index.html
npx cap sync android

# Open in Android Studio to build/sign the APK or AAB
npx cap open android
```

The app ID (`com.yourname.tetonor` in `capacitor.config.json`) must be updated before publishing and cannot be changed after the first Play Store release.

## Game Architecture

The entire game state lives in a few module-level variables:

- `puzzle` — the active puzzle: `{ grid[], strip[], pairs[], hidden (Set), userEntries[] }`
- `selectedCell` — index (0–15) of the currently active grid cell, or `null`
- `entryNums`, `entryOp`, `stripSelected` — the in-progress entry for the selected cell

### Puzzle data model

- **`pairs`**: 8 pairs `{ a, b, sum, prod }`. Each pair contributes two grid cells: one for `sum` (op `+`) and one for `prod` (op `×`).
- **`grid`**: 16 shuffled entries `{ value, pair, op }` — the target values shown in the 4×4 grid.
- **`strip`**: 16 numbers (`pairs.flatMap(p => [p.a, p.b])`), sorted ascending. Indices in `hidden` (a `Set`) are shown as `?` tiles.
- **`userEntries[i]`**: `{ a, b, op, si1, si2 }` where `si1`/`si2` are strip indices (used to track per-tile usage counts, not just per-value).

### Key invariant

Each pair must be used **exactly twice across all 16 cells** — once with `+` and once with `×`. `checkAll()` validates both that arithmetic is correct and that this pair rule holds.

### Strip state tracking

`updateStripState()` counts usages by **strip index** (via `si1`/`si2` in `userEntries`), not by value. This correctly handles the case where two strip tiles have the same value. Tiles used twice get the `.used` class (greyed out); tiles used once get `.used-once` (amber outline).

### Assist mode

When the first strip number is picked and Assist is on, `pickStripNum()` scans `userEntries` for a cell that already used that value, then auto-fills the partner number and flips the operator (`+`↔`×`).

### Difficulty

Controlled by the `DIFF` config object — affects the numeric range of generated values and the number of hidden `?` tiles (5 / 7 / 11 for easy / medium / hard).
