# Bee Twist — Product Requirements Document

## Overview

Bee Twist is a browser-based word puzzle game that combines two established games:

- **NYT Spelling Bee** — a honeycomb letter grid where every word must use the center letter
- **Text Twist** — a word-length hint panel showing how many words remain and their letter counts

The primary innovation over Spelling Bee is visibility: players can see exactly how many words they haven't found and how long each one is. This makes it easier to know when to keep trying, what word lengths to target, and to learn which words are accepted.

The project also serves as a learning vehicle for AI-enabled development workflows and SDLC skills.

---

## Problem / Motivation

NYT Spelling Bee gives players no indication of how many words remain or their lengths. This makes it difficult to know when you've exhausted your ideas versus when you're close to complete, and offers no structured way to learn words you missed. Bee Twist fills that gap with a Text Twist-inspired word list that reveals structure without giving away the answers.

---

## MVP

The MVP is a single, fully playable puzzle session with the core game loop. No scoring, no daily puzzle, no persistence.

### Game Rules (Spelling Bee)

- 7 letters arranged in a honeycomb: 1 center (required) letter, 6 surrounding letters
- Every submitted word must contain the center letter
- Words must be at least 4 letters long
- Letters may be reused any number of times
- Pangrams (words using all 7 letters) are highlighted when found

### Puzzle Data

- A small set of curated, hardcoded puzzles is bundled with the app
- Each puzzle includes its letter set and pre-computed answer list
- Word validation checks the player's submission against the answer list — no runtime dictionary needed

### UI Layout

Side-by-side layout:

```
+----------------------+----------------------+
|  [ Honeycomb       ] |  4-letter words:     |
|   O  O  O  O  O  O  O|  ____  ____  ____    |
|                      |  5-letter words:     |
|  [ _ _ _ _ _ ]      |  _____  _____        |
|  [ Submit ] [Clear]  |  6-letter words:     |
|                      |  ______              |
+----------------------+----------------------+
```

### Letter Input

Players can enter letters by:
- Typing on the keyboard
- Clicking hexagon tiles in the honeycomb

### Word-Length Hint List

- Unfound words are displayed as dash patterns grouped by word length (e.g., `____ ____ ____` under "4-letter words")
- When a word is found, its dash pattern is replaced with the revealed word
- Pangrams are visually distinguished when revealed

### Session State

- No persistence — game state resets on every page load
- No scoring, ranks, streaks, or daily puzzle in MVP

---

## Non-Functional Requirements

### Testing

Tests must be a reliable indicator that the app is functioning as desired. This enables safe, confident changes by both developers and AI. High confidence in correctness is the standard — not coverage percentages for their own sake.

- **Vitest** covers game logic and data model (unit tests)
- **Playwright** covers user interactions and game states (UI/integration tests)
- Tests follow Given/When/Then structure and test behavior, not implementation details
- Vitest coverage reporting must be configured before the first implementation sprint; threshold to be established once initial tests are written

### ESLint Complexity Rule

Cyclomatic complexity is capped at **5** per function via ESLint's `complexity` rule. This enforces small, focused functions consistent with the low-complexity engineering principles in `CLAUDE.md`. This rule must be configured before the first implementation sprint.

### Code Quality

- ESLint + Prettier with default configs (per `CLAUDE.md`)
- TDD: tests are written before implementation

---

## Technical Stack

See `CLAUDE.md` for the full engineering principles.

| Concern | Choice |
|---|---|
| UI framework | React + Vite (browser-based, runs locally) |
| Unit testing | Vitest |
| UI/integration testing | Playwright |
| Linting / formatting | ESLint + Prettier |

---

## Future Ideas

The following are post-MVP possibilities. No priority order or timeline is implied.

1. **Reveal center letter** — show the required center letter in all unguessed dash patterns as an optional hint
2. **Dictionary definitions** — an icon next to each unguessed word that reveals its Merriam-Webster definition on click
3. **Persist puzzles and solutions** — save letter sets and answer lists (e.g., localStorage or a data file) so puzzles are easier to manage, expand, and curate
4. **Scoring and levels** — points per word, pangram bonus, and rank tiers modeled on NYT Spelling Bee (e.g., Beginner → Good → Amazing → Genius → Queen Bee)
5. **Cloud deployment** — host the app publicly so others can play
