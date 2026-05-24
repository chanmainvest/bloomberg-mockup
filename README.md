# Bloomberg AMD reference assets

Captured Bloomberg Terminal screens for **AMD US Equity** (session May 20–21, 2026). This folder is a **standalone git repository** (MIT license).

**Interactive mockup:** [https://chanmainvest.github.io/bloomberg-mockup/](https://chanmainvest.github.io/bloomberg-mockup/)

## Contents

| Path | Description |
|------|-------------|
| `index.html` | Interactive mockup (GitHub Pages entry point) |
| `mockup_data.json` | Screen metadata + hotspots (embedded into `index.html` at build time) |
| `screenshots/` | Images named `PAGE_CODE_tab_sub_tab.jpg` |
| `pdfs/` | Exported PDFs (HELP, BTST, GP, …) |
| `charts/` | `GP_price_chart.svg` |
| `notes/pasted_notes.md` | Cleaned copy-paste from email bodies |
| `pages_catalog.md` | Page code → description table |
| `image_index.json` | Per-file metadata (page code, tab, blob id) |
| `capture_timeline.json` | All screens in capture order |

## Regenerate from downloads

Source mail attachments: `../outlook_agent/downloads/hevangel@yahoo.com/`

From the **bloomberg_mockup** repo root:

```powershell
uv run python scripts/build_mockup_data.py
uv run python scripts/build_index_html.py
cd reference
git add index.html mockup_data.json .nojekyll
git commit -m "Update GitHub Pages mockup."
git push
```

Regenerate organized reference assets from downloads:

```powershell
uv run python scripts/merge_image_index.py
uv run python scripts/organize_bloomberg_reference.py
```

OCR hotspot cache (optional, ignored by git): `ocr_cache.json`

## License

MIT — see [LICENSE](../LICENSE).
