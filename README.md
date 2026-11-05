# Crimson Chess

Crimson Chess is a small chess game that lives in a single HTML file. You play against a computer opponent on a fantasy themed purple-and-gold board, and that's pretty much the whole idea. No accounts, no installs, no build step. Open the file and you're playing.

I wanted something that felt a little moody and pretty but still loaded instantly on a phone, so everything (the rules, the opponent, the styling) is in one place.

## Getting started

1. Download `Crimson Chess.html`.
2. Open it in any modern browser.
3. Make your move.

That's it. You can also drop the file on any static host and share the link, since there's nothing to run on a server.

## How to play

Tap or click one of your pieces. The squares it can legally move to light up with a small golden dot. Eating your opponents piece gets marked by a red circle. Tap a highlighted square and the move is made. If you change your mind, tap a different piece to switch.

The top of the screen tells you whose turn it is and lets you know when you're in check. When a king is under attack, its square glows red. The last move is softly highlighted so you can always see what just happened.

### The controls

- **Play White / Play Black** lets you pick your side. Choosing Black flips the board and lets the computer open.
- **Apprentice / Mage / Archmage** sets how strong the computer plays (more on that below).
- **Undo** takes back your last move and the computer's reply, so you're back to your turn.
- **Flip** turns the board around if you'd rather see it from the other side, depending if you want black or white.
- **New game** The whole game starts over

### Rules that are in

The usual rules are all here: every piece moves the way it should, you can't leave your own king in check, and the game recognizes checkmate and stalemate. Castling works on both sides (and it won't let you castle out of, through, or into check). En passant works too.

### Rules that aren't

I kept this one lean, so a few things are missing. Pawns always promote to a queen automatically, with no menu to pick something else. There's also no draw by threefold repetition, the fifty-move rule, or insufficient material. If a game goes in circles, you'll have to call it yourself.

## The opponent

The computer looks a few moves ahead using a classic minimax search with alpha-beta pruning, which is a fancy way of saying it imagines moves and replies, then throws out lines that clearly can't be better. It judges positions mostly by counting material, with small bonuses for pieces and pawns that sit near the center or push forward.

The three levels differ in how deep it looks:

| Level | Search depth | Personality |
|-------|--------------|-------------|
| Apprentice | 1 move | Short-sighted and a bit random. Good for beginners and for a relaxed game. |
| Mage | 2 moves | Spots simple tactics. A fair fight for casual players. |
| Archmage | 3 moves | Looks further ahead and plays noticeably tighter. |

Be realistic about the Archmage, though. It's not an engine like Stockfish. It has no opening book and no deep endgame knowledge, and it can still be outplayed by a patient human. That's partly the fun of it.

## Under the hood

Everything is plain HTML, CSS, and vanilla JavaScript with no libraries. A few things that might be useful if you want to poke around:

- The board is stored as a flat array of 64 squares, and each position keeps track of whose turn it is, castling rights, and any en passant target.
- Legal moves are generated first as "pseudo-legal" moves, then filtered by checking whether your own king would be left under attack.
- The computer thinks inside a short timeout so the page has a moment to redraw before it starts calculating. At Archmage depth on an older phone, you may notice a brief pause.
- The layout is responsive and respects the safe areas on phones with notches.

## Ideas for later

If I keep working on it, these are the things I'd add first:

- A choice of piece when promoting a pawn
- Draw detection for repetition, the fifty-move rule, and insufficient material
- A move list, so you can review the game afterward
- A smarter evaluation and move ordering, so the computer can look deeper without slowing down
- Saving the game so it survives a page refresh

## License

Do what you like with it. If you build something fun on top of it, I'd love to hear about it.
