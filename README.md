# Anki Difficulty Tagger

🔗 **AnkiWeb**  
https://ankiweb.net/shared/info/1300169603

---

## What this add-on does

**Anki Difficulty Tagger** automatically assigns **difficulty tags** to cards based on your review behavior.  
Instead of manually tagging cards as “easy” or “hard”, this add-on analyzes your answers and applies tags consistently.

It is designed to help you:

- Identify difficult cards quickly
- Filter decks by difficulty
- Adjust study strategy using objective criteria

---

## Core Features

- 🏷 Automatically assigns difficulty tags to cards
- 📊 Uses review outcomes (Again / Hard / Good / Easy)
- 🔁 Updates tags dynamically as difficulty changes
- 🪶 Lightweight and fast
- 🧩 Works with any deck and note type
- ⚙️ Fully configurable tagging rules

---

## How It Works

1. You review cards as usual in Anki
2. Based on your answers, the add-on evaluates card difficulty
3. Difficulty tags are added or updated automatically
4. Old difficulty tags can be removed or replaced

This keeps difficulty information **always in sync with your actual performance**.

---

## Why Use Difficulty Tags?

Difficulty tags allow you to:

- Create filtered decks like:
  - `tag:hard`
  - `tag:easy`
- Focus extra time on weak areas
- Avoid wasting time on cards you already know well
- Monitor long-term learning progress

Unlike static tags, these tags **evolve with your learning**.

---

## Installation

### From AnkiWeb (recommended)

1. Open Anki  
2. Tools → Add-ons → Get Add-ons  
3. Enter the code from AnkiWeb  
4. Restart Anki  

👉 https://ankiweb.net/shared/info/1300169603

---

### Manual (GitHub)

1. Download or clone this repository
2. Place it in:

   `Anki2/<profile>/addons21/anki-difficulty-tagger/`

3. Restart Anki

---

## Configuration

Open:

**Tools → Add-ons → Anki Difficulty Tagger → Config**

Available options include:

- Enable / disable tagging
- Tag names for each difficulty level
- Rules for assigning difficulty
- Whether to remove old difficulty tags
- Scope (review-only or include other actions)

Settings are applied automatically during normal reviews.

---

## Usage

- Simply review cards as usual
- Tags are updated automatically in the background
- No manual action is required

You can then use the Browser to:

- Search by difficulty tag
- Create filtered decks
- Analyze difficult cards in bulk

---

## Performance & Safety

- No background polling
- Operates only during review events
- Does **not** modify scheduling or intervals
- Safe to enable on large collections

---

## Compatibility

- Anki 24.x
- Anki 25.x
- Windows / macOS / Linux

---

## License

MIT License

---

## Author

Created by **@yuwayanagitani**

---

## Related Add-ons

- **AI Grader** – AI-based grading of answers
- **Anki Bar Graph** – Visualize recent review activity
- **AI Card Explainer** – Add explanations to cards

These add-ons can be combined to build a **data-driven Anki workflow**.
