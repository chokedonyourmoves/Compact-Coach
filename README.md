# Compact Coach

Chess analysis overlay for chess.com and lichess. Shows you arrows on the board while you play — because sometimes you want a second opinion.

![screenshot](screenshot.png)

## What it does

- Draws arrows on the board suggesting your best moves
- Stockfish 19 running as a WASM worker, bundled in the extension
- Different personalities — Best, Human, Aggressive, Positional, Endgame, Brilliant Focus
- ELO slider (1320–2850) if you want human-like mistakes instead of perfect play
- Pick how many arrows to show (1–3)
- Draggable widget, dark theme
- Works on chess.com and lichess.org

## Install

You'll need Chrome (or any Chromium browser).

1. Download or clone this repo
2. Go to `chrome://extensions`
3. Turn on **Developer mode** (top right)
4. Click **Load unpacked** and pick the `compact-coach` folder
5. Open a chess.com or lichess game

That's it. No build step, no dependencies, no npm install.

## Why it's built this way

The obvious approach — running Stockfish in a Web Worker from a content script — doesn't work. Content-script workers inherit the page's CSP, and chess.com's CSP blocks `WebAssembly.instantiate()`. So the engine has to live somewhere else.

The workaround: the content script injects a hidden `<iframe>` pointing at `engine-host.html`, which is an extension-origin page. That iframe spawns the worker from `chrome-extension://…/stockfish.js`. Because the worker belongs to the extension origin, MV3's `'wasm-unsafe-eval'` CSP exception applies and the WASM actually compiles.

## TL;DR

cheat for chess and lichess that lets you see the best move wiht different personality. Brilliants will be marked in gold with !! exclamation mark and it only shows one arrow. it also goes the same for human mode.
