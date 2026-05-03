# 🌿 PlantID Pro — Website & Plant Knowledge Base

This repository contains two things:

1. **`index.html`** — Landing website for the PlantID Pro iOS app (bilingual VI/EN)
2. **`data/plants.json`** — Comprehensive plant knowledge base used as a fallback when PlantNet API is unavailable

## Deploy as GitHub Pages

1. Go to **Settings → Pages** in this repo
2. Set **Source** to `main` branch, `/ (root)` folder
3. Your site will be live at `https://<username>.github.io/<repo-name>/`

To use a custom domain (`plantidpro.app`):
- Add a `CNAME` file containing `plantidpro.app`
- Configure DNS at your registrar: CNAME `www` → `jaytran-prog.github.io`

## Plant Knowledge Base (`data/plants.json`)

The JSON file contains detailed bilingual (VI/EN) data for Vietnamese and tropical plants:

- Scientific names + family
- Identification labels (for matching PlantNet API results)
- Bilingual descriptions
- Care guide (water, light, soil, fertilizer, temperature)
- Toxicity warnings
- Common diseases with symptoms and treatment
- Fun facts
- Identification tips

### iOS App Integration

The app fetches this file as a fallback when:
- PlantNet API exceeds its 500 req/day free limit
- No internet connection

See `RemotePlantDatabase.swift` in the iOS project for the fetch + cache logic.

## File Structure

```
PlantIDWeb/
├── index.html          # Landing page
├── privacy.html        # Privacy policy
├── terms.html          # Terms of use
├── data/
│   └── plants.json     # Plant knowledge base (fallback database)
└── assets/             # Screenshots, icons (add as needed)
```

## Adding More Plants

Each plant entry in `plants.json` follows this schema:

```json
{
  "id": "unique-id",
  "name": "Tên tiếng Việt",
  "nameEn": "English Name",
  "scientificName": "Genus species",
  "family": "Family name",
  "emoji": "🌿",
  "labels": ["scientific name", "common name 1", "common name 2"],
  "description": "Mô tả tiếng Việt...",
  "descriptionEn": "English description...",
  "care": {
    "water": "...", "waterEn": "...",
    "light": "...", "lightEn": "...",
    "difficulty": "...", "difficultyEn": "...",
    "temperature": "20–35°C"
  },
  "toxic": false,
  "funFact": "...",
  "funFactEn": "...",
  "diseases": [...]
}
```

The `labels` array is critical — it must include all names that PlantNet API might return for this plant (scientific name, common names, genus name).
