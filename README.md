# Surgical Recall — Rapid Fire

A single-file flashcard site for the *Surgical Recall* rapid-fire questions.
330 cards across 47 chapters, all embedded in `index.html` — no build step, no
dependencies, no network calls.

## Run it

Open `index.html` in a browser, or serve the folder:

```
python3 -m http.server 8000
```

## Using the deck

- **Tap the card** (or press space) to flip it; space again moves to the next card.
- **Arrow keys** change cards; up/down hide and show the answer.
- **S** stars the current card. "Starred only" filters the deck down to them.
- **Reset done** clears your done marks. It asks once before clearing — the first
  click arms it, the second confirms, and it disarms itself after 4 seconds.
  Stars are not affected.

## What's remembered

Revealing a card's answer marks it **done**; done cards show a ✓ in the corner,
and the header counts how many of the cards currently in view are done. Progress
is saved to `localStorage` as you go and restored on reload:

| Key | Holds |
| --- | --- |
| `surgicalrecall.starred` | starred cards |
| `surgicalrecall.progress` | done cards, current card, chapter, order mode, starred-only, shuffle seed |

Both are per-browser and per-origin — they don't sync across devices, and
clearing site data wipes them.

Shuffling stores a seed rather than the shuffled order, so reopening the page
rebuilds the same sequence and drops you back on the card you were on. Clicking
**Shuffle** again draws a new seed and reshuffles.
- **Swipe** left/right on touch devices to move between cards.
- The chapter dropdown filters by chapter; **Shuffle** and **Book order** set the
  card sequence.

## Editing the cards

Card data lives in the `<script id="cards" type="application/json">` block in
`index.html`. Each entry is:

```json
{"c": 17, "t": "FLUIDS AND ELECTROLYTES", "p": "Name the most likely diagnosis:", "q": "…", "a": "…"}
```

`c` is the chapter number, `t` the chapter title (title-cased at runtime), `p` an
optional prompt stem shared by a group of questions, `q` the question and `a` the
answer.

Saved stars are keyed by chapter + stem + question, so adding, removing, or
reordering cards won't scramble them. Editing the text of a card that's already
starred does drop that one star.
