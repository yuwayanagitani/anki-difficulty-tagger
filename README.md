# Anki Difficulty Tag Assigner

This Anki add-on automatically assigns a 5-level difficulty tag to notes based on review statistics (lapses / interval / ease). Use these tags to filter, suspend, generate filtered decks, or inspect which notes are giving you trouble.

- Repository: yuwayanagitani/anki-difficulty-tag-assigner
- Description: This add-on automatically assigns a 5-level difficulty tag to notes based on review statistics (lapses / interval / ease).

Table of contents
- Features
- How it works (overview)
- Tag format
- Installation
- Usage
- Configuration
- Examples
- Developer / Contributing
- License

Features
- Computes a difficulty score per note using review statistics (lapses, review interval, ease).
- Maps scores to one of five difficulty levels (1 = very easy, 5 = very hard).
- Applies human-friendly tags to notes (configurable prefix and behavior).
- Configurable thresholds and weights so you can tune what "hard" means for your collection.
- Option to update tags automatically during review and/or reassign tags for the whole collection.

How it works (overview)
The add-on collects per-note review statistics (such as number of lapses, recent review intervals and ease factors), computes a composite "difficulty score" and maps that score into five buckets. The composite score is based on:
- Lapse rate (how often the card has been marked as lapse)
- Typical review interval (short intervals often indicate harder cards)
- Ease (low ease indicates more difficulty)

The exact weighting and mapping are configurable (see Configuration). The goal is to provide a stable difficulty signal so you can act on groups of similarly-difficult notes.

Tag format
By default tags take the form:
- difficulty/1 — Very easy
- difficulty/2 — Easy
- difficulty/3 — Medium
- difficulty/4 — Hard
- difficulty/5 — Very hard

Both the prefix (`difficulty`) and the numeric range can be configured.

Installation
There are two common installation methods:

1) Install from this repository (manual)
- Download this repository (Download ZIP).
- Extract the folder and place it inside your Anki add-ons directory:
  - On Windows: %APPDATA%\Anki2\addons21\
  - On macOS: ~/Library/Application Support/Anki2/addons21/
  - On Linux: ~/.local/share/Anki2/addons21/
- Restart Anki.

2) Install from an Add‑on ID (if published)
- If this add-on is published to AnkiWeb, you can install using its Add-on ID in Anki: Tools → Add-ons → Get Add-ons… and enter the ID.

Usage
- After installing and restarting Anki the add-on will begin to evaluate cards as you review them and assign difficulty tags based on the collected statistics.
- Most users will see tags applied automatically over time as cards collect review history.
- To re-evaluate all notes (bulk reassign), use the add-on's "Recalculate difficulty tags" action if available in the Tools → Add-ons menu, or run the included script (see Developer section) to do a one-time pass over the collection.

Configuration
Configuration is intentionally flexible. Typical options include:

- enabled: true/false — Enable automatic tagging during reviews.
- tag_prefix: "difficulty" — Tag prefix used for created tags.
- levels: 5 — Number of difficulty levels (default 5).
- overwrite_existing: true/false — Whether to replace existing difficulty tags or keep them.
- weights:
  - lapse: 0.5
  - interval: 0.3
  - ease: 0.2
- thresholds: optional explicit thresholds for mapping score → level
- lookback_days: how many days of reviews to consider (default: 90)

Example configuration (JSON)
```json
{
  "enabled": true,
  "tag_prefix": "difficulty",
  "levels": 5,
  "overwrite_existing": true,
  "weights": {
    "lapse": 0.5,
    "interval": 0.3,
    "ease": 0.2
  },
  "lookback_days": 90
}
```

Mapping notes to levels (example)
A simple conceptual mapping:
- Compute normalized metrics:
  - lapse_rate ∈ [0,1] (higher → harder)
  - normalized_interval ∈ [0,1] (longer interval → easier; invert if desired)
  - normalized_ease ∈ [0,1] (higher ease → easier; invert if desired)
- Composite score:
  score = w_lapse * lapse_rate + w_interval * (1 - normalized_interval) + w_ease * (1 - normalized_ease)
- Map score into 5 buckets (quintiles) or use custom thresholds.

Examples / Use cases
- Create a filtered deck containing only difficult cards:
  tag:difficulty/4 OR tag:difficulty/5
- Run targeted review: study only difficulty/5 cards until they move down to difficulty/3.
- Monitor progress: track how many cards move from difficulty/5 → difficulty/1 over time.

Developer / Contributing
Contributions, bug reports and suggestions are welcome.

Suggested steps to develop locally:
1. Clone the repository:
   git clone https://github.com/yuwayanagitani/anki-difficulty-tag-assigner.git
2. Install development dependencies (if any).
3. Use a local copy in your Anki addons21 directory to iterate quickly.
4. Open a PR with a clear description of the change and include tests where appropriate.

Notes for maintainers
- Be careful modifying tag names: renaming a prefix or changing numeric levels will leave stale tags in users' collections. Provide a migration path if tags are changed.
- Keep default weights conservative so beginner users don't see surprising re-tagging.

Troubleshooting
- If you don't see tags applied immediately, allow some review history to accumulate (or use the bulk reassign tool).
- If tags are not created at all, check the add-on is enabled in Tools → Add-ons and that your Anki version is compatible.
- If something breaks, check Anki's Tools → View Logs for Python exceptions.

Compatibility
- Anki 2.1+ (recommended). If you are running a very old or pre-2.1 Anki, this add-on may not work.

Security & privacy
- This add-on only reads review statistics from your local Anki collection and writes tags to your local notes. It does not transmit your data externally.

License
See the LICENSE file in this repository for license details.

Acknowledgements
- Inspired by the need to quickly identify tricky notes and focus study where it matters.

If anything in this README is unclear or you'd like a different layout or more technical details (code examples, CLI usage, or default algorithm), tell me which sections you'd like expanded and I will update the README.
