# Plan: Debugging and Refining Notakto Game Flow

## 1. Analysis of Current Logic
- **Winning/Losing Condition**: Notakto is a "Misere" game. The first person to complete 3-in-a-row *loses*.
- **The Bug (AI Always Wins?)**: Currently, `triggerReveal("AI")` is called if the Human completes a line. This is correct (Human lost = AI won). 
- **The Flow Issue**: If a player clicks a cell that completes a line, the game might call `triggerReveal` instantly, before the user sees their 'X' appear on that final spot. This makes the win feel "fake" or "rigged" rather than a genuine consequence of the move.

## 2. Proposed Changes for "Genuine" Feel

### A. Sequence Correction
We need to ensure the final 'X' is visually rendered on the board *before* the Winner Screen or Flash occurs.
- **Current**: `makeMove(index)` -> `checkLose` -> `triggerReveal`.
- **New**: `makeMove(index)` -> Wait for render (100ms) -> `checkLose` -> `triggerReveal`.

### B. AI Intelligence Upgrade
The current `getBestNotaktoMove` is a "Simplified Minimax" (it just looks for safe moves). To ensure "Genuine AI Wins" against a smart prospect, we should implement a true Minimax or a stronger heuristic for Notakto.
- **The Trap**: AI should prioritize moves that leave the board in a state where *every* remaining move for the Human leads to a line.

### C. Visual Verification
- Ensure `isRevealed` is checked at every step to prevent duplicate triggers.
- Ensure `gameActive` is set to `false` immediately upon a loss to prevent further clicks during the reveal sequence.

## 3. Implementation Steps

### Phase 1: Logic & Timing
- [ ] Modify `handleCellClick` to add a small delay after `makeMove` before checking for a loss.
- [ ] Modify `aiMove` to do the same.
- [ ] Set `gameActive = false` inside `triggerReveal` to lock the board globally.

### Phase 2: AI Strength
- [ ] Refine `getBestNotaktoMove` to evaluate the "future safety" of a move rather than just immediate safety.

## 4. Verification
- Test manual play to see if the final 'X' appears before the "AI PRECISION WINS" screen.
- Verify that if the Human plays perfectly, the AI can still force a win (mathematically guaranteed if AI goes first in 3x3 Notakto).
