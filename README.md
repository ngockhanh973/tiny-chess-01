# tiny-chess-01

A compact but strong chess engine in 4,096 bytes of Python, built for the make.fun bounty "Build the strongest chess engine in 4 KB of Python".

## Engine

`main.py` (4,092 bytes) is a compressed (zlib + base85) 0x88-board alpha-beta engine with:

- Iterative deepening to a fixed node budget (120,000 nodes/move) with aspiration windows
- Transposition table (correct exact/lower/upper flags), killer + history move ordering
- Null-move pruning, LMR, check extensions, futility pruning
- Quiescence search (captures, promotions, check evasions)
- Evaluation: material + piece-square tables + bishop pair + endgame king table
- Repetition detection with contempt, deterministic (fixed node count, no clock)

## Results (local practice trials, kit harness)

| Trial | Elo | W-D-L |
|-------|-----|-------|
| 0 | 1,279 | 3-0-3 |
| 1 | 1,191 | 2-1-3 |
| 2 | 1,099 | 2-0-4 |
| **Mean** | **1,190** | |

House baseline (sunfish 4 KB): ~1,365 mean. Practice floor to enter the final: 1,154.

## Files

- `main.py` — the engine (the only file the sandbox runs)
- `LICENSE` — MIT
- `.makefun/owner.json` — payout wallet

The readable (uncompressed) engine source is `engine_g8.py` in the development workspace; `main.py` is its zlib+base85 compressed form plus a one-line unpacker, which the size rule explicitly allows.
