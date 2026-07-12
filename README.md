# Simple Reversi Game

> A browser-based Reversi (Othello) game with a computer opponent and cross-session save/resume, built in React and TypeScript.

## Tech Stack
- Frontend: React 18 + TypeScript, React Router (hash routing)
- Build tooling: Vite
- Persistence: Remote key-value endpoint (env-configured) for game state save/resume
- Deployment: GitHub Pages via `gh-pages`

## What It Does
Play Reversi against a computer opponent, choosing your disc color before the game starts. Move validation and scoring follow standard Reversi rules. Login with a username/password to save game state remotely and resume an in-progress game from any device — the app checks for and restores an unfinished game on login rather than starting over.

## Architecture
- `src/components` — `MainPage` (disc color + login) and `game-page/GamePage` (the board and turn loop)
- `src/logic/validLogic.ts`, `updateBoard.ts`, `handleTurn.ts` — move validation, board updates, and turn handling
- `src/logic/getComputerMove.ts` — computer opponent move selection
- `src/logic/calculateScore.ts` — disc counting / scoring
- `src/logic/gameStateLogic.ts` — fetch/upload game and account state to the remote endpoint
- `src/logic/validateCredentials.ts` — login input validation

## Key Implementation Details
- Game state (board, turn, chosen disc color) is persisted server-side per username, so a match survives a closed tab or a different device.
- Computer opponent move selection and Reversi's flip/validity rules are implemented from scratch rather than via a game library.

## Running Locally
```bash
npm install
npm run dev
```
Requires a `.env` with `VITE_ENDPOINT_URL` and `VITE_GAMEKEY` pointing at a compatible key-value endpoint for save/resume to work; the board and computer opponent work without it.

Build and deploy to GitHub Pages:
```bash
npm run deploy
```
