# SLSA — Sri Lankan Students' Association (UMN) website

A static site for GitHub Pages. No build step, no dependencies — just HTML/CSS/JS.

```
slsa-website/
├─ index.html         ← the whole site (HTML + CSS + JS inline)
├─ data/
│  └─ events.csv      ← the calendar reads this
└─ media/             ← all photos
   ├─ board.jpg                 group photo
   ├─ gayal.jpg … milan.jpg     board portraits (used in “Board”)
   └─ card-*.jpg                illustrated posters (used in “Photos”)
```

## Deploy on GitHub Pages
1. Push this folder to a repo (everything at the repo root).
2. Repo **Settings → Pages → Build from branch → `main` / root**.
3. Done — it’s live at `https://<you>.github.io/<repo>/`.

## Edit the events / calendar
Open **`data/events.csv`**. One row per event:

| column | required | notes |
|---|---|---|
| `date` | ✅ | `YYYY-MM-DD` |
| `title` | ✅ | event name |
| `time` | — | e.g. `6:00 PM – 8:00 PM` |
| `location` | — | venue / room |
| `category` | — | `Social` `Food` `Cultural` `Sports` `Meeting` (sets the colour dot) |
| `description` | — | a sentence or two |
| `rsvp` | — | a link (e.g. a Google Form). Shows an **RSVP** button only if filled in |
| `image` | — | optional — add this column + a path like `media/food-night.jpg` to show a photo on the event |

Wrap any field that contains a comma in `"double quotes"` (already done in the sample).
The calendar opens on the next upcoming event automatically.

**Prefer a Google Sheet?** In Sheets: *File → Share → Publish to web → (your sheet) → CSV*, copy the link, and paste it into `CONFIG.csvUrl` near the top of the `<script>` in `index.html`.

## Wire up the “Join our mailing list” popup
In `index.html`, find `CONFIG.mailing` at the top of the `<script>`:
- **Easiest with capture:** make a free form at [formspree.io](https://formspree.io) and paste its endpoint into `formspree`. Emails then land in your inbox / Google Sheet.
- **No setup:** leave `formspree` blank and paste your sign-up Google Form link into `googleForm` — the button opens it in a new tab.

Until you set one of these, the popup still works and shows a thank-you (and logs the email to the browser console).

## Swap photos
Drop new files into `media/` and keep the same names, or update the paths in `index.html`
(portraits are plain `<img>` tags in the Board section; the Photos gallery is the `GALLERY` array in the `<script>` — add `{src:'media/your.jpg', cap:'Caption'}` to add event photos).

## Preview locally
Because the calendar uses `fetch()`, double-clicking the file won’t load events. Run:
```
python -m http.server
```
then open `http://localhost:8000`.

---
Placeholders to replace: the contact email (`slsa@umn.edu`) and the RSVP / mailing-list form links.
