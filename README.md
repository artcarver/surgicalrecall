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
