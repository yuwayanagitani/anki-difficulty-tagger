# Difficulty Tag Auto‑Assigner (5 levels)

Automatically assigns **5 difficulty tags** to your *notes* based on your learning stats (**lapses / interval / ease**).

- Tags: `VeryHard`, `Hard`, `Medium`, `Easy`, `VeryEasy`
- Runs in the background with a progress window
- Settings are edited via a **custom GUI** (no extra Tools “Settings” item)

---

## What it does

This add-on evaluates each reviewed card (`reps > 0`) and chooses **one** difficulty tag, then:

1. Removes any existing difficulty tags from the note  
2. Adds the newly judged tag to the note  
3. Updates the note in the collection

**Decision order (important):**  
`VeryHard → Hard → VeryEasy → Easy → Medium`

That order matters: earlier rules win.

---

## How to run

Open Anki, then:

**Tools → Auto-assign difficulty tags (5 levels)**

You’ll be prompted for a search query:

- Leave empty → tag **all** cards in the collection  
- Enter a query (e.g., `deck:MyDeck is:due`) → tag only matching cards

The add-on updates notes, then calls `mw.reset()` to refresh.

---

## Settings

Open the add-on’s config screen:

**Tools → Add-ons → (Difficulty Tag Auto‑Assigner) → Config**

This opens the custom GUI.

### Very Hard
- **Minimum lapses (≥)**: `very_hard_lapses_min`
- **Max ease (<)**: `very_hard_ease_max_pct` (%)

### Hard
- **Minimum lapses (≥)**: `hard_lapses_min`
- **Max ease (<)**: `hard_ease_max_pct` (%)

### Easy
- **Max lapses (≤)**: `easy_lapses_max`
- **Min interval (≥)**: `easy_ivl_min` (days)
- **Min ease (≥)**: `easy_ease_min_pct` (%)

### Very Easy
- **Min interval (≥)**: `very_easy_ivl_min` (days)
- **Min ease (≥)**: `very_easy_ease_min_pct` (%)

> Note on “ease”: Anki stores it as `factor` (e.g., 250% is stored as 2500).  
> This add-on’s GUI uses **percent** (e.g., `250` = 250%).

---

## Defaults

The shipped defaults are:

- VeryHard: lapses ≥ 5 **or** ease < 200%
- Hard: lapses ≥ 3 **or** ease < 230%
- Easy: lapses ≤ 0 **and** interval ≥ 21 days **and** ease ≥ 250%
- VeryEasy: interval ≥ 90 days **or** ease ≥ 280%
- Medium: everything else

---

## Notes / Tips

- Tags are applied **per note**, so if multiple cards belong to the same note, the note ends up with the tag computed from the last processed card for that note (by loop order).
- New/never-reviewed cards (`reps == 0`) are skipped.
- If you already use difficulty tags, make sure they match the exact tag names above, since the add-on removes only those five.

---

## Troubleshooting

- **Nothing happens / 0 processed**  
  Your search may match no cards, or all matched cards may have `reps == 0`.

- **Tags don’t look updated immediately**  
  The add-on calls `mw.reset()` after completion, but if you still don’t see changes, try syncing or reopening the browser.

