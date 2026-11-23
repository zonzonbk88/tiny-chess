# tiny-chess — a 4 KB chess engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/zonzonbk88/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/zonzonbk88/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original chess engine written for the make.fun bounty
[tiny-chess-01](https://make.fun/bounty/tiny-chess-01): the strongest engine
that fits in 4,096 bytes of Python. `main.py` is the whole engine; it plays
the house gauntlet through the trial env (`MAKEFUN_ENV_URL`), one game after
another, and exits when every game is over.

## How it plays

- **Board**: 0x88 mailbox, pseudo-legal generation with make/unmake and a
  king-safety test, covering castling, en passant and promotions.
- **Search**: negamax alpha-beta with iterative deepening under a fixed
  budget of 50,000 nodes per move — never a clock, so the same position
  always gets the same move. Quiescence covers captures and promotions,
  with full evasions when in check.
- **Ordering**: MVV-LVA for captures, promotion bonuses, two killer moves
  per ply for quiet ones.
- **Evaluation**: material plus hand-written piece-square tables (packed
  one value per character), maintained incrementally as moves are made;
  the king table blends middlegame and endgame values by remaining
  material phase.

`main.py` as committed is produced from a readable source with the kit's
own `makefun compress` (an LZMA-packed entrypoint, as the bounty rules
allow); the source travels with the entry's transcript bundle.
