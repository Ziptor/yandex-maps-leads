---
name: yandex-maps-leads
description: Collect local business leads from Yandex Maps by city and category, including prospects whose listings lack a standalone website, and export a CSV.
---

# Yandex Maps leads

Use the bundled [yamaps_parser](https://github.com/dmikhaylov/yamaps_parser) in the parser subdirectory next to this file. Use the requested city and business category. Ask only for missing details that materially affect the search.

From the parser directory, initialize its dependencies with `uv sync --locked` and `uv run playwright install chromium` as needed. The upstream project uses uv to manage Python dependencies.

Start with a limited search, for example:

```powershell
uv run yamaps_parser.py "Казань" "барбершоп" --no-grid --limit 20 --output "<absolute CSV path>"
```

Use the default grid search when broader area coverage is needed. Keep email extraction off unless requested. For leads without a standalone site, keep rows with a blank `site` field or a `site` link that only points to a social profile, messenger or directory. Keep `social`, `phone`, `reviews` and `url` in the shortlist, and deduplicate by listing ID. Label the output as businesses with no standalone site listed. When actual site absence matters, verify shortlisted businesses by name and city or business phone. Report raw and filtered row counts.
