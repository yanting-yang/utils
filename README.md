# arXiv Fetcher

A small browser utility for generating arXiv API and listing URLs, importing papers, viewing JSON and readable results, and counting papers by date. It uses plain HTML, CSS, and JavaScript with no build step or package installation.

## Run locally

Open `index.html` in a modern browser and follow **arXiv Fetcher**, or open `arxiv_fetcher.html` directly.

## Load papers

Select categories in Step 1, then select **Generate URLs** to create one XML API link plus a recent HTML listing link for each selected category. With no categories selected, the selection defaults to `cs.*`; wildcard categories use the corresponding listing, such as `cs.*` → `cs`.

**Max Results** and **Sort By** apply only to the XML API link. HTML listing pages use arXiv's default pagination. Open a generated link and save the XML response or HTML page for import.

Choose one of two input options in Step 2: **Import Data**:

1. **XML:** Upload a saved arXiv API XML response, including files without an extension (such as `query`). Files are parsed as XML regardless of their filename.
2. **HTML:** Upload a saved arXiv listing page, or paste its source into the **HTML Source** tab in Step 2. Pasted HTML is parsed automatically.

Import status appears in Step 2. Uploading a file keeps the generated links in Step 1 available.

## View and filter results

Step 3 shows its result tabs and date controls after an import contains papers. Before importing, or after empty or invalid input, it shows an import hint.

For XML imports, the tabs are **Raw XML**, **Statistics**, **JSON**, and **Parsed Result**, in that order. HTML imports show **Statistics**, **JSON**, and **Parsed Result**. If Raw XML was active when HTML is imported, the view switches to Statistics. **JSON** shows structured paper data and **Parsed Result** shows readable text without Last updated or Published lines. Their **Copy** buttons copy the displayed output. Switching result tabs keeps the Step 2 **HTML Source** input visible.

Use **Date field** to choose **Last updated** (the default) or **Published** for XML data. HTML data uses **Listing date**, extracted from listing headings where available. Missing dates appear as **Unknown date**; HTML JSON records use `null` when no listing date is available.

The date selector starts at **All dates**. Select a date, or **Unknown date** when available, to filter both JSON and Parsed Result, including copied text. Loading new input resets the filter.

The **Statistics** tab counts papers by the selected date field across the entire loaded dataset. Selecting a date to filter the output does not reduce these counts. These are counts of loaded entries, including any cross-listings or replacements present in the input.

Statistics also includes an expandable date-count table for each main category, with its paper total in the summary and the first category open initially. These tables use the selected date field and the full dataset. Each paper belongs to exactly one group, using the XML primary category or HTML primary subject. HTML primary subjects use the category code in their final parentheses when available, otherwise the cleaned subject label. Papers with a missing or blank main category appear under **Unknown category**; secondary categories are not used.

## Files and maintenance

- `index.html`: Home page linking to the utility.
- `arxiv_fetcher.html`: Application markup, styling, parsing, and browser event handlers.
- `AGENTS.md`: Guidance for contributors and coding agents.

There is no build system or committed test runner. Validate changes in a browser with small XML and HTML samples, checking URL generation, parsing, date filtering, statistics, tab switching, and copying. File import and pasted HTML can be checked locally.
