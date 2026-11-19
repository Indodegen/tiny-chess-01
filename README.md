# Tiny Chess — strongest chess engine in 4 KB of Python

[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Indodegen/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Indodegen/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01)

An original 0x88 chess engine written from scratch for the
[make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01):
build the strongest chess engine in 4 KB of Python.

## How it plays

`main.py` is the whole engine (Python 3.13, standard library only). It talks
to the gauntlet env over HTTP (`POST /game`, `POST /move`) and picks every
move with a real search:

- **0x88 board** with full legal move generation: castling, en passant,
  promotions, check and checkmate detection.
- **Negamax + alpha-beta**, iterative deepening to a **fixed node budget**
  (no clock — a replayed trial plays the same moves).
- **Quiescence search** on captures, so it does not blunder into tactics.
- **Transposition table** (incremental Zobrist hashing), **MVV-LVA +
  killer + history** move ordering.
- **Evaluation**: material + piece-square tables (own values), bishop-pair
  bonus, endgame king table, tempo.

The readable source is `engine.py`; `main.py` is the packed entrypoint
produced by `makefun compress` (LZMA), within the 4,096-byte cap.

## License

MIT — see `LICENSE`.
