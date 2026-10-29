# Product Requirements Document: Snake

**Status:** Implemented
**Product:** Snake (`snake-game.html`)

## 1. Overview

Add a standalone, browser-playable Snake game to the repository. The player steers a snake around a bounded board, eats food to grow and earn points, and avoids the walls and the snake's own body. The game should be easy to open and play without installing dependencies.

## 2. Goals

- Provide a complete, responsive Snake game in a single HTML file.
- Support keyboard play on desktop and visible directional controls for touch and pointer users.
- Make game state, score, pause, restart, and end conditions clear.
- Save the player's best score locally without changing Memory Game scores.
- Keep core controls usable with keyboard and assistive technology.

## 3. Non-goals

- Multiplayer, online leaderboards, accounts, or network access.
- Power-ups, obstacles, multiple maps, or adjustable difficulty.
- Changes to the existing Memory Game.
- Frameworks, external libraries, audio dependencies, or a build process.

## 4. User stories

1. As a player, I can start, pause, resume, and replay a round.
2. As a desktop player, I can steer using the arrow keys or WASD.
3. As a touch or pointer player, I can steer using on-screen directional controls.
4. As a player, I can see my current score and best score.
5. As a player, I understand when I collide, win, or need to restart.

## 5. Functional requirements

### Gameplay

- Use a 20-by-20 board with a snake that starts at length three and moves at a steady, readable pace.
- Place food only in unoccupied cells. Eating food grows the snake and adds 10 points.
- End the round when the snake hits a wall or itself. If the snake fills every board cell, declare a win instead of placing more food.
- Reject an immediate reversal into the snake's current direction. Process at most one new turn per movement step so quick key presses cannot create an invalid turn sequence.
- Provide clear ready, running, paused, game-over, and won states.
- The main action starts a round, pauses or resumes it, and starts a fresh round after a win or game over.

### Controls and accessibility

- Arrow keys and WASD steer while playing. Space starts, pauses, or resumes the game.
- Provide labeled on-screen directional buttons for touch and pointer input.
- Ensure all buttons can be reached and activated by keyboard with visible focus.
- Announce status changes and score updates through accessible text. Do not rely on canvas visuals or color alone to communicate game state.
- Keep the board legible on narrow screens and at browser zoom levels.

### Score persistence

- Display current and best scores.
- Store the best score under a Snake-specific local-storage key; never modify the Memory Game's `memoryGameScores` key.
- Continue gameplay if browser storage is unavailable, and report storage errors to the console.

## 6. Implementation constraints

- Implement the game in `snake-game.html` with inline CSS and JavaScript.
- Use browser-native HTML, CSS, Canvas, and JavaScript only; no external resources or dependencies.
- Keep game state and score handling separate from the Memory Game.
- Respect reduced-motion preferences; gameplay movement must not depend on CSS animation.

## 7. Acceptance criteria

1. Opening `snake-game.html` directly in a modern browser shows a ready-to-play game without setup.
2. Starting a round moves the snake; food increases both its length and score by 10.
3. Arrow keys, WASD, and on-screen controls steer without allowing an immediate reversal.
4. Space and the main action correctly pause and resume without resetting the round.
5. Wall and self-collisions end the round; the replay action starts a fresh game. Filling the board results in a win.
6. The best score persists across reloads using a Snake-specific key, and Memory Game score data is unaffected.
7. Keyboard focus, touch controls, and status announcements work; the board fits narrow viewports.
8. The game requires no external dependencies, network access, or build step.

## 8. Validation checklist

- Test initial ready state, start, pause, resume, and replay.
- Test keyboard directions, on-screen directions, and rejection of reverse turns.
- Test eating food, wall collision, self-collision, score saving, and high-score display.
- Verify the board is responsive and controls remain keyboard and touch accessible.
- Confirm the `memoryGameScores` local-storage value is unchanged.
