# Watering Log

A small web app for keeping a home plant collection watered, set up for growing in Singapore's climate.

It is a single HTML page with no build step and no server: open it in a browser, or publish it with GitHub Pages.

## What it does

- **Today's watering round.** Shows which plants are due or overdue today, overdue first, with a progress ring and a one-tap **Watered** button (with Undo) for each plant.
- **Missed waterings.** Overdue plants are flagged with how many days late they are, and the most overdue plant is called out under the headline.
- **This week.** A seven-day strip showing which plants come due on each day.
- **Plant details.** Each plant keeps its photo, species, watering interval, where it grows, sunlight, preferred fertilizer and feeding schedule, soil and pot, care notes, and a five-week watering history that marks overdue days.
- **Plant finder.** When adding a plant, search a built-in guide of about 40 common plants and the care fields fill in, with the watering interval adjusted for where the plant grows (air-conditioned room, indoors, sheltered outdoors or full sun).

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole app: markup, styles and script |
| `starter-plants.json` | The plant list loaded on a browser's first visit |
| `README.md` | This file |

## Run it locally

The starter list is loaded with `fetch`, which browsers block for pages opened straight from the file system. Serve the folder instead:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000.

Opened directly as a file, the app still works but starts with an empty list.

## Publish with GitHub Pages

1. Create a new repository on GitHub and upload these files to its root (or push them with git).
2. In the repository, go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, and save.
4. After a minute the app is live at `https://<your-username>.github.io/<repository-name>/`.

## Where your data is kept

Plants and waterings are saved in the browser's local storage, on that device only. They are not uploaded anywhere and do not sync between devices or browsers. Clearing the site's data in the browser removes them.

On the first visit in a browser, the app loads `starter-plants.json`. To change the starting list, edit that file before publishing. Each plant looks like this:

```json
{
  "id": "p-lemon",
  "name": "Lemon",
  "species": "Citrus × limon",
  "every": 1,
  "setting": "sun",
  "sun": "full",
  "fertilizer": "Citrus fertilizer with magnesium and iron",
  "fertEvery": "Every 4–6 weeks, year-round",
  "soil": "Well-draining potting mix, large pot with drainage holes",
  "notes": "Care notes shown on the plant's details sheet.",
  "location": "",
  "lastWatered": "2026-11-01",
  "history": ["2026-11-01"],
  "photo": "",
  "created": "2026-11-01"
}
```

- `every`: days between waterings
- `setting`: `ac` (air-conditioned room), `indoor`, `shade` (outdoors, sheltered) or `sun` (outdoors, full sun)
- `sun`: `full`, `bright`, `partial` or `low`
- `lastWatered` and `history`: dates as `YYYY-MM-DD`; `lastWatered` may be `null`

## Features that need Claude

The app was first built as a Claude artifact. Three features depend on that environment and stay hidden when the page runs anywhere else:

- syncing plants across devices
- looking up care details for any plant with Claude
- identifying a plant from its photo

Perenual plant data imported in that version is not included here.

## About the care information

Watering intervals and care notes are general guidance for Singapore's hot, humid climate, not measured values for your plants. Check the soil before watering, and confirm details with a reference such as [NParks Flora & Fauna Web](https://www.nparks.gov.sg/florafaunaweb). Each plant's details sheet links to searches on NParks, the Missouri Botanical Garden and the Royal Horticultural Society.

## Credits

Type is set in [Geist](https://vercel.com/font) (SIL Open Font License), loaded from Google Fonts.
