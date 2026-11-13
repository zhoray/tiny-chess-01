# Verdant Gambit

Verdant Gambit is my tiny-chess-01 entry. The board uses 0x88 square indices, with the unused edge bits making boundary checks simple.

The search is negamax with alpha-beta pruning. Iterative deepening spends a fixed 30,000-node allowance on each move. Quiescence continues the tactical lines through captures and promotions, and a checked side searches its available evasions.

Checks earn an extra ply. Late quiet moves may begin at reduced depth and receive a full search when they improve the current bound. A transposition table reuses position results, and capture ordering compares the values of the pieces involved.

Material and piece-square values form the static score. The king's square value blends between middlegame and endgame tables according to remaining non-pawn material. Passed pawns also gain a bonus that rises with their progress.

The build process shortens identifiers, compresses the source with LZMA, and writes the compressed bytes as base85 text. The resulting `main.py` is a self-contained launcher and payload, measuring **4,087 bytes**.

On practice trial-1, the entry earned Elo 1087, finishing with three wins, two draws, and eleven losses. The shared-VM run took about 1,947 seconds overall. Average thinking time was around 2.3 seconds per move against a ten-second allowance.

The entry is licensed under the MIT License; see [LICENSE](LICENSE).

## Checks

Move generation matches the reference totals 8,902, 197,281, 97,862, and 43,238 across the starting setup and three benchmark positions. Source and packed builds are compared for evaluation, state updates, perft, and selected search moves. Tactical positions and search-value regressions cover key decisions, while a short protocol smoke case checks the driver's move exchange.
