# Satyam Agarbatti Reports (offline-first PWA)

A responsive dashboard built around `Satyam_Agarbatti_Data.xlsm`. Includes dashboard charts, order register, daily summary, SKU master, business calendar, workbook import, record editing, validation, CSV/JSON export, and a read-only User interface mode.

## Run locally

Because browser security blocks some PWA features from `file://`, serve this folder through a local HTTP server:

```bash
python -m http.server 8080
```

Open `http://localhost:8080`. On a desktop, install it from the browser's install option. On Android Chrome, use **Add to Home screen**. The shell and data are cached for offline use after the first successful visit. Workbook import uses SheetJS from jsDelivr on first use; visit online once before trying to import `.xlsm` offline.

## Demo role mode

- **User mode**: read-only UI.
- **Admin mode**: choose Admin in the role switch and enter `admin123`.

This passcode is only a demo convenience and is not secure authentication. The app stores data in browser `localStorage` on that device. It does not sync across devices. Do not publish confidential business data in this static build.

## Workbook import behaviour

Imports `tblMaster` (preferred) or `CSV` / `Master Data` as order records, plus `SKU Master` and `Business Calendar`. Imported rows replace the current local rows. Export a JSON backup before replacing important data.

## VBA/macros note

Web browsers cannot execute Excel VBA macros embedded in `.xlsm`. The app implements browser-native equivalents for recalculating dashboard summaries, validation, and exports. Any other business-critical VBA logic must be documented and reimplemented explicitly before treating reports as a verified replacement for Excel.

## GitHub Pages deployment

1. Create a repository (the existing project repository can be reused if appropriate).
2. Upload all files in this folder to the repository root.
3. In GitHub, open **Settings → Pages** and select **Deploy from a branch**, branch `main`, folder `/ (root)`.
4. Wait for the published URL. Use HTTPS for PWA installation and service-worker offline caching.

A workflow is included in `.github/workflows/pages.yml` to publish from the `main` branch when GitHub Pages is configured for GitHub Actions.

## Recommended production upgrade

For secure online admin/user access and multi-device sync, connect Supabase (Auth + Postgres + Row Level Security) and use offline local changes with a sync queue. This starter intentionally does not create a backend or incur service costs.
