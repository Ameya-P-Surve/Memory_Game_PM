# Product Requirements Document: Dark Theme for Memory Game

**Status:** Proposed
**Date:** October 29, 2026
**Product:** Memory Game (`memory-game.html`)

## 1. Overview

Add an optional dark theme to the existing browser-based memory game. Players can switch between light and dark appearances without interrupting a game. The selected appearance should be remembered on the same browser, while the game continues to work as it does today.

The game is a self-contained HTML file with inline CSS and JavaScript. It currently has light-colored page, controls, card faces, score list, and win dialog surfaces, alongside existing CSS custom properties for some theme colors.

## 2. Goals

- Let players switch between light and dark themes from the game screen.
- Make the initial theme follow the operating-system preference unless the player has previously chosen a theme.
- Persist an explicit theme choice across reloads without changing or overwriting game scores.
- Keep all game content legible and usable in both themes.
- Preserve existing game behavior, layout responsiveness, keyboard play, and accessibility.

## 3. Non-goals

- Changing card matching, scoring, timers, grid sizes, or game rules.
- Changing how best scores are calculated, displayed, or stored.
- Adding dependencies, a build step, or additional pages.
- Adding custom themes or per-element appearance settings.

## 4. User stories

1. As a player who prefers a darker screen, I can enable dark theme while playing so the game is comfortable to view.
2. As a player, I can tell which theme is active and switch back to light theme at any time.
3. As a returning player, I see my previously selected theme when I reopen the game.
4. As a keyboard or assistive-technology user, I can find, operate, and understand the theme control.
5. As a player, I can keep playing and access my scores regardless of the selected theme.

## 5. Functional requirements

### Theme selection

- Add a clearly labeled theme toggle to the existing game interface; it must be available before or during a game.
- The control must indicate the current state programmatically and visibly. It must be keyboard operable and have an accessible name that communicates its action or current theme.
- On a first visit with no saved choice, use the device's `prefers-color-scheme` preference. If that preference is unavailable, use light theme.
- When the player changes the theme, apply it immediately without reloading or resetting the game.
- Save the player's explicit choice using a dedicated local-storage key. Do not reuse, modify, or clear the `memoryGameScores` key.
- On later visits, use the saved choice in preference to the device preference. If saved preference access fails or contains an unsupported value, use the system preference when available and otherwise use light theme.

### Theme coverage

Both themes must style all visible game surfaces consistently, including:

- Page background and primary text.
- Statistics panel, grid-size buttons, and their active/hover/focus states.
- Unflipped and flipped card faces, matched-card state, and focus indicator.
- Best-scores area and empty-state message.
- Win dialog, dialog text, and play-again button.

Maintain sufficient contrast in both themes: at least WCAG 2.2 AA contrast for normal text (4.5:1) and for meaningful control boundaries, focus indicators, and other non-text UI (3:1). Do not rely on color alone to communicate game state.

## 6. UX and visual direction

- Keep the existing layout, spacing, typography, and card-flip effect. The theme should change colors, not the game's structure or interaction model.
- Use a dark page background with readable, appropriately distinct surfaces for panels, cards, and the dialog. Preserve the visibility of card symbols and the question-mark card backs.
- Keep primary actions, active grid selection, hover feedback, and keyboard focus easy to distinguish in either theme.
- If theme transitions are animated, keep them subtle and respect the user's reduced-motion preference.

## 7. Compatibility and implementation constraints

- Implement the feature in the existing `memory-game.html` file using its inline CSS and JavaScript; do not introduce external dependencies.
- Prefer extending the existing CSS custom-property approach so shared colors change together. Replace hard-coded surface and interaction colors where needed so no major component remains unintentionally light in dark theme.
- Keep theme initialization and event handling separate from game state and score handling.
- Do not alter card data, grid initialization, timer and move logic, win handling, or score serialization.
- Preserve the current responsive layouts and mouse and keyboard gameplay.

## 8. Acceptance criteria

1. With no saved theme, the game opens in the operating system's preferred theme; when that preference is unavailable, it opens in light theme.
2. The theme control is visible, keyboard operable, and exposes the active state to assistive technology.
3. Switching themes updates every surface listed in **Theme coverage** immediately and does not reload, reset, or otherwise interrupt an active game.
4. Reloading after an explicit selection restores that selection even if the operating-system preference differs.
5. Theme selection uses a separate storage key; existing best scores remain available and unchanged after theme changes and reloads.
6. Light and dark themes meet the contrast requirements above, including focus and control states.
7. In both themes, a player can play and win on both 4x4 and 6x6 grids; card flips and matches, moves, timer, rating, win dialog, play-again action, and best scores continue to work.
8. The game remains usable at narrow viewport widths and with keyboard-only navigation.
9. No external dependency or additional setup is required to open and play the game.

## 9. Validation checklist

- Test initial appearance with system light and dark preferences and with no saved choice.
- Test switching themes during a game, refreshing, and reopening the file; confirm the explicit choice persists.
- Confirm saved best scores survive theme changes and remain readable in both themes.
- Play through one game of each grid size in each theme, including the win dialog and play-again flow.
- Check keyboard navigation, visible focus, and the theme control's announced name and state.
- Check contrast and narrow-screen layout in both themes.
