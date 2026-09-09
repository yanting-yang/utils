# Repository guidance

## Scope and structure

This repository contains static browser utilities. `index.html` links to `arxiv_fetcher.html`, which keeps its HTML, CSS, and JavaScript in one file. There is no package manager, build step, or committed test runner.

## Editing conventions

- Keep changes focused and preserve unrelated local files and user edits.
- Use native browser APIs and the existing JavaScript style, including the `$` and `$$` DOM helpers. Avoid adding dependencies or build tooling for small features.
- Render imported paper content as text using `textContent` or form values. Do not insert untrusted XML or HTML into the live page with `innerHTML`.
- Preserve XML API and per-category recent listing URL generation, including wildcard-to-listing mapping and the default category. Maximum results and sorting apply only to the XML API URL.
- Preserve both input options: XML upload and HTML upload or paste. Keep import status in Step 2 without replacing generated Step 1 links.
- Scope tab switching independently to each step. Keep HTML Source in Step 2 and the Step 3 order: Raw XML, Statistics, JSON, Parsed Result.
- Show Step 3 tabs, panels, and date controls only when the imported dataset contains papers; otherwise show the import hint. Hide Raw XML for HTML imports, switching to Statistics if Raw XML was active.
- Keep JSON, Parsed Result, and their copied text synchronized with the date filter. Statistics should count the complete loaded dataset using the selected date field.
- Keep per-category statistics as expandable date-count tables with category totals and the first category initially open. Assign each paper to exactly one group using XML `arxiv:primary_category` or HTML `primary_subject`. For HTML, prefer a final parenthesized category code, then the cleaned primary-subject label. Use Unknown category when the explicit main category is missing or blank; never fall back to secondary categories.
- Reset the date filter when loading new input. Treat missing dates explicitly as unknown rather than inventing dates from paper IDs.
- Update `README.md` when user-facing behavior or local usage changes.

## Validation

Open the page in a browser; no build is required. Use small local XML and HTML samples to check affected behavior. For date-related changes, include several papers on one date, another date, and a missing date; check both XML date fields, HTML listing dates, filtered JSON and readable output, full-dataset statistics, copying, and reset on new input. Check tab visibility for XML, HTML, empty, and invalid input, and inspect the browser console for errors.

Keep validation proportional to the change. Do not introduce a test framework for a small UI edit. Report which checks ran and any validation limits.
