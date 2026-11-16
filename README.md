[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Jhoni1098/tiny-chess-01-v04/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Jhoni1098/tiny-chess-01-v04/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess-01 v04

A compact chess engine for the [make.fun](https://make.fun/bounty/tiny-chess-01) tiny-chess-01 competition (main.py ≤ 4,096 bytes, Python 3.13 stdlib only, deterministic).

## Design

- **Board:** 0x88, signed pieces, incremental material+PST eval (house-formula PSTs, tapered endgame king PST, bishop-pair bonus).
- **Search:** negamax + PVS + quiescence (captures/promotions, check evasions, delta pruning, check extension), transposition table, 2 killers/ply, MVV-LVA ordering, fixed 80,000-node budget, iterative deepening (depth 1 unlimited, deeper iterations share the budget; an aborted iteration is dropped whole).
- **Opening book:** 50 entries covering the 15 practice openings (white move 9 + black replies vs the house's 500k-node engine), keyed by a polynomial hash of the move sequence. The book move is played when the position matches; otherwise the engine searches.
- **Deterministic:** fixed node budget, no clock, no randomness.

## Local practice Elo (kit grade-local, 6 games per trial)

| Trial | Elo | W | D | L |
|-------|-----|---|---|---|
| 0 | 1279 | 3 | 0 | 3 |
| 1 | 1809 | 5 | 1 | 0 |
| 2 | 1451 | 4 | 0 | 2 |
| **Mean** | **1513** | | | |

Beats v02's mean (1338) and the sunfish baseline (~1365). Perft verified (startpos d4 197281, kiwipete d3 97862).
