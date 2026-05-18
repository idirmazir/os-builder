# OS // Builder — Personal OS Intake

A single-page intake form for capturing client information used to build a bespoke "Personal OS" — a private, dark-mode, scoreboard-style tracking app. Captures profile, time horizon, categories, goals, system behaviour, and 12-month vision across 21 modules, then exports a print-perfect PDF build spec the client emails over for handover.

## Stack

Plain HTML, CSS, and vanilla JavaScript in a single file. No build step. No runtime dependencies.

## Local preview

Open `index.html` directly in any modern browser, or serve the folder:

```bash
npx serve .
# or
python3 -m http.server 8000
```

## Deploy to Vercel

### Option 1 — GitHub + Vercel UI (recommended)

1. Push this folder to a new GitHub repository.
2. Go to <https://vercel.com/new> and import the repo.
3. Hit **Deploy** — no settings to change. Vercel auto-detects a static site and serves `index.html` at the root.

### Option 2 — Vercel CLI

```bash
npm i -g vercel
vercel
```

Follow the prompts. Subsequent deploys: `vercel --prod`.

## Configuration

The recipient email for completed intakes lives in `index.html`. Search for `idirmazir@gmail.com` and replace both occurrences (the visible link text and the `mailto:` href) in the SUBMIT block markup. The form does not send mail itself — the SUBMIT button triggers the browser's print-to-PDF; the client saves the PDF locally and emails it to that address.

## Files

- `index.html` — the entire app (HTML + CSS + JS)
- `vercel.json` — minimal config (clean URLs)
- `.gitignore` — common ignores
- `README.md` — this file

## How it works

- **Autosave** — every keystroke persists to the browser's `localStorage`. The form survives reload.
- **21 modules** — paginated, with a sticky bottom tab strip for jumping. Category-detail modules (Health, Wealth, etc.) wake up only when the matching category is ticked in Module 03.
- **Auto-detect tracking** — in goal blocks, the "How to track this goal" suggestion is inferred from the goal text (numbers → Number, "every day" → Yes/no daily, "settle / built / sold" → Stages, etc.).
- **Quality gate** — clicking SUBMIT validates field-level completeness (name + role, future end date, 4–7 categories ranked, 5 fully-filled goals, aesthetic + frequency + one-number chosen, outcome vision ≥ 50 chars, vague-target heuristic). Lists specific gaps before letting the client export anyway.
- **Print-to-PDF** — submit opens the browser's print dialog with a stylesheet that strips chrome, inverts to white, and pages each module. Client picks "Save as PDF" as destination.
