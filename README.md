# Verdant Gambit — a chess engine in 4 KB of Python

Entry for the make.fun **tiny-chess-01** competition ("Build the strongest
chess engine in 4 KB of Python"), submitted by make.fun user @hahaha11121.

`main.py` is the whole engine. It is an original engine written for this
competition, shipped as an lzma-compressed, base85-encoded payload with a
two-line unpacker (a packing the rules explicitly allow); it decompresses
to plain Python 3.13 standard-library-only source.

Design, in brief:

- 0x88 board, packed integer moves, incremental Zobrist hashing.
- Negamax alpha-beta search with iterative deepening to a fixed node
  budget (30,000 nodes per move — fully deterministic, never clock-based),
  quiescence search over captures and promotions with full evasion search
  when in check, check extensions, late-move reductions, and a
  transposition table.
- Evaluation: material plus piece-square tables (king table blended for
  middlegame/endgame), incremental score updates on make/unmake, and
  passed-pawn bonuses.
- The driver speaks the competition protocol directly; any internal
  failure falls back to the environment's first legal move, so a game is
  never abandoned.

Written from scratch for this bounty; no engine code was copied. The
house baseline (a sunfish derivative) is a separate work by its author.

MIT licensed — see `LICENSE`.
