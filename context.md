# Repository Context

## What this project does

This repository contains a small, responsive browser-based Memory (also called Concentration) game. A player flips cards to find matching pairs, aiming to finish with fewer moves and a faster time. The game supports 4x4 and 6x6 boards.

## How it works

The game is implemented as a self-contained HTML page in [`memory-game.html`](./memory-game.html), with its CSS and JavaScript embedded in the same file. It does not require a framework, package installation, build step, or external dependency.

The page creates a shuffled set of emoji cards for the selected board size. Players can flip cards with a mouse or keyboard; the game tracks moves, elapsed time, matches, and a star rating. Completing a board opens a win dialog, and players can start another round or switch board sizes.

Best scores are stored in the browser's local storage under the `memoryGameScores` key. This means scores belong to that browser's local storage and are not shared across browsers or devices.

## Main files

- [`memory-game.html`](./memory-game.html) — The playable game and its implementation.
- [`README.md`](./README.md) — Features, basic instructions, and local run guidance.
- [`PRD_dark_theme.md`](./PRD_dark_theme.md) — Proposed requirements for a dark theme. This is a specification; it does not mean dark-theme functionality has been implemented.
- `.gitignore` — Git ignore configuration.

## Running the game

Open `memory-game.html` in a modern browser. Alternatively, from the repository directory, run `python3 -m http.server 8000` and visit `http://localhost:8000/memory-game.html`.

## What “GHCP” stands for

The repository name includes `GHCP`, but the README and game source do not define what that abbreviation means. Its expansion cannot be confirmed from the project files.
