# Tetonor

**Tetonor** is a number logic puzzle. Each of the 16 cells in the grid holds a target number. Your job is to figure out which pair of numbers from the bottom strip produces it — and whether by addition or multiplication.

---

## The core rule

The strip holds 16 numbers, arranged as 8 pairs. Every pair **(a, b)** appears exactly twice in the grid:

- once as **a + b**
- once as **a × b**

So every number in the strip is used in exactly two cells. That constraint is what makes the puzzle solvable by logic.

---

## How to play

### 1. Select a grid cell
Click any cell in the 4×4 grid to select it. The target number is shown large at the top of the cell.

### 2. Pick two numbers from the strip
Click any two tiles in the bottom strip. The order doesn't matter.

### 3. Pick an operator
Click **+** or **×**. As soon as both numbers and an operator are chosen the entry confirms automatically.

You can pick the operator before, between, or after the two numbers — any order works.

### 4. Check your work
When you're ready, click **Check**. Correct cells turn green, wrong ones turn red. You don't have to fill all 16 cells before checking.

To fix a wrong cell, click it to select it, then click **Clear** and re-enter.

---

## The strip

The strip numbers are sorted in ascending order. Tiles change appearance as you use them:

| Appearance | Meaning |
|---|---|
| Normal | Unused |
| Amber outline | Used once (one cell filled so far) |
| Greyed out | Used twice — both cells complete |

Clicking a greyed-out or amber tile with no cell selected will **pulse** the cells that used it, so you can find your work.

---

## Hidden numbers (?)

Some tiles in the strip are hidden and shown as **?**. You must deduce their values from the grid.

- **Click a ? tile** to enter your guess. You can enter any number — wrong guesses are accepted and validated later via Check.
- Once revealed, the tile behaves like any other strip tile.
- **Long-press a revealed tile** to clear it and any cells that used it, so you can start that tile's guess over.

The hidden tiles, like all strip numbers, appear in ascending order relative to their position.

---

## Difficulty

| Level | Strip range | Hidden tiles |
|---|---|---|
| Easy | 2 – 20 | 5 |
| Medium | 5 – 35 | 7 |
| Hard | 10 – 50 | 11 |

Select difficulty from the **New Puzzle** dropdown. Starting a new puzzle while one is in progress will ask for confirmation.

---

## Assist

When **Assist** is enabled (on by default), picking a strip number that's already been used in one cell will automatically fill in its pair partner and the remaining operator for the current cell.

You can toggle Assist off if you prefer to work without hints.

---

## Reveal

Stuck? Click **Reveal** to show the full solution. This disables the Check button for the current puzzle.

---

## Tips

- **Start with products.** Multiplication produces larger, more distinctive numbers, which are often easier to factor uniquely.
- **Use the pair rule.** When you find two strip numbers whose sum and product both appear in the grid, you can fill both cells with confidence. For example, if 3 and 7 are in the strip and both 10 and 21 appear in the grid, that pair is solved.
- **Amber tiles are your friends.** A tile used only once still has one cell left. Focus on those pairs to narrow down the remaining cells.
- **Hidden tiles last.** Leave ? tiles until surrounding cells constrain what value they must be. Often only one number fits the gap.
