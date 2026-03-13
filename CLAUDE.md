# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a personal sandbox repository used to experiment with Claude Code. It has no build system, test runner, or CI pipeline. The Visual Studio solution (`ClaudeCodeTest.sln` + `ClaudeCodeTest.mdproj`) is an empty generic MSBuild project shell — it contains no actual source code and is not built or run.

## Current Content

- **`flappy-tetris.html`** — A self-contained, single-file HTML5 canvas game. No dependencies, no build step. Open directly in a browser to run. All game logic lives in the `<script>` tag of this file.

### flappy-tetris.html architecture

The game uses a circular-world model:

- **World grid**: `world[wc][row]` — a 2D array of `WORLD_COLS × ROWS` cells storing landed block colors. World columns wrap modulo `WORLD_COLS`.
- **Scroll**: `scrollX` (pixels) increases each frame. `toWC(screenCol)` converts a fixed screen column to the current world column, handling the wrap.
- **Active piece**: fixed at screen column `PIECE_COL`. Has continuous `pixelY` + `vy` (Flappy Bird physics). `SPACE` sets `vy = FLAP_V` and rotates the shape CW.
- **Collision** (`collides(shape, pixelY)`): maps each piece block's screen column through `toWC` to check the world grid.
- **Landing**: step `pixelY` down 1 px at a time until `collides` is true, then call `lockPiece()` which writes blocks into the world grid.
- **Game over**: piece lands in row ≤ 2, or a scrolling world column moves a block into the piece's current position.

### Oyun Mantığı (Türkçe Özet)

- Ekran sabit, dünya yatay kayan dairesel bir ızgara (`world[wc][row]`).
- Tetris parçası ekranın belirli bir sütununda (`PIECE_COL`) sabit durur; Flappy Bird fiziğiyle (yerçekimi + zıplama) yukarı/aşağı hareket eder.
- `SPACE` tuşu parçayı yukarı fırlatır ve saat yönünde döndürür.
- Dünya her kare sola kayar; parça, dünya sütunlarına çarpışma kontrolüyle etkileşime girer.
- Parça yere değince `lockPiece()` bloğu dünya ızgarasına yazar.
- Oyun biter: parça üst 2 satıra çıkarsa veya kayan dünya parçanın konumuna çarparsa.
