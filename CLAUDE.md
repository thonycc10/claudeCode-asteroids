# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running

Vanilla HTML5 canvas game: no build, bundler, dependencies, linter, or tests. Open `index.html` directly, or serve it with `npx serve .` (http://localhost:3000). README and in-game text are in Spanish.

## Architecture

Everything lives in `game.js` (loaded by `index.html`, which holds a fixed 800x600 `<canvas id="canvas">`).

- **Input**: `keys` / `justPressed` maps keyed by `e.code`; read through `pressed()`.
- **Entities**: classes `Bullet`, `Asteroid`, `Ship`, `Particle`. The space is toroidal; positions wrap with the `wrap` helper.
- **Size tables**: `RADII`, `SPEEDS`, `POINTS` are indexed by asteroid size 1-3 (index 0 unused). Size 3 is large (20 pts), size 1 is small (100 pts); asteroids split into smaller sizes when destroyed.
- **Global state**: `ship`, `bullets`, `asteroids`, `particles`, `score`, `lives`, `level`, plus `state` (`'playing' | 'dead' | 'gameover'`) and `deadTimer`.
- **Loop**: `requestAnimationFrame(loop)` calls `update(dt)` then `draw()`. Helpers: `spawnAsteroids`, `initGame`, `nextLevel`, `explode`, `killShip`.

## Notes

- Power-ups and the shooting-star asteroid were removed in recent commits, but README.md still mentions them.
- `.agents/`, `.claude/`, and `skills-lock.json` are untracked tooling, not part of the game.
