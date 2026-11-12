
# Reference Validator

Researchers waste hours manually checking whether each citation is real, whether the DOI resolves,
and whether the bibliographic details match the actual source. This skill automates that audit and
delivers a Word report (for reading) and an Excel workbook (for filtering/sorting the raw data).

## What it produces, per reference (minimum)

- **Relevance confidence (0–100%)** — how well the cited work supports the claim at its citation
  location. This is *AI judgment*, grounded on the source's title/abstract, and is labeled as such.
- **Does the DOI exist?** — resolved against Crossref/DataCite (HTTP 200 vs 404).
- **Does the DOI's record describe the same work?** — title match.
- **Do author names and their order match** the online record.
- **Do the other components match** — publication year, article title, journal/container title,
  volume, issue, page range — each with its own verdict (Match / Partial / Mismatch) and score.
- **Component breakdown for everything** — even references that can't be audited online (books,
  print-only articles, websites) get their components parsed out and documented.

Plus meta-analysis (including **% of references with no DOI / unauditable**), retraction flags,
preprint-vs-published detection, and citation-hygiene checks (duplicates, uncited references,
orphan in-text citations).

## Critical environment note — how lookups happen

The sandboxed shell **cannot reach doi.org / Crossref / DataCite** (the proxy returns 403). So all
metadata lookups MUST be done with your own web fetch tool (`web_fetch` / equivalent), NOT with
curl or Python `requests` inside the shell. You fetch each record, save the raw JSON into a
`lookups/` folder, and the offline Python scripts read those cached files. The Python does the
parsing, matching, scoring math, and document generation — it never touches the network.

`https://api.crossref.org/works/{DOI}` returns full JSON on a plain GET (no special headers), which
is why `web_fetch` works on it. See `references/lookup_api.md` for exact endpoints and fields.

## Workflow

Work through these steps in order. Use a scratch working directory (e.g. `./rv_work/`) for
intermediate files, and write final deliverables to the user's folder.

### 1. Get the manuscript to text

```bash
python scripts/extract_manuscript.py "<INPUT_FILE>" -o rv_work/manuscript.txt
```

Read `rv_work/manuscript.txt`. If extraction is poor (e.g. a scanned PDF yields little text), tell
the user and offer OCR or a cleaner file.

### 2. Extract references + in-text citations into references.json

Read the whole manuscript and build `rv_work/references.json` following the schema in
`references/references_schema.md`. For every reference:

- Assign the `id` used in the bibliography (the number, or a running index for author–year styles).
- Copy the full `raw_text` of the reference entry.
- Classify `type`: journal-article, conference, book, chapter, report, thesis, dataset, preprint,
  website, or other.
- Parse components into `parsed`: authors (as a list, preserving order), year, title,
  container_title (journal/book/proceedings), volume, issue, pages, doi (or null), publisher.
- Find **every in-text citation** of that reference and record the surrounding sentence(s) in
  `in_text.contexts`, and the total `in_text.citation_count`. This context is what the relevance
  score is judged against, so capture the actual claim being supported, not just the marker.
- Record any in-text citation markers that have **no** matching bibliography entry in the top-level
  `orphan_citations` list.

Be careful with both numeric ([12], superscripts) and author–year ((Smith et al., 2020)) styles.

### 3. Look up each reference online (via your fetch tool) and cache to lookups/

Create `rv_work/lookups/`. For each reference:

- **If it has a DOI:** fetch `https://api.crossref.org/works/{DOI}`. Save the raw JSON response to
  `rv_work/lookups/{id}.json`. If the fetch returns a 404 / "Resource not found", instead write
  `{"http_status": 404, "not_found": true}` to that file. If Crossref 404s but you suspect a
  DataCite DOI (datasets, some books), try `https://api.datacite.org/dois/{DOI}` and save that.
- **If it has no DOI (discovery):** query
  `https://api.crossref.org/works?query.bibliographic=<title + first author>&rows=3` (URL-encode the
  query). Inspect the top candidate(s). If a candidate clearly matches the reference (title and
  first author align), save that response but add `"doi_source": "discovered"` at the top level of
  the saved JSON, e.g. `{"doi_source":"discovered","message-type":"work-list","message":{...}}`. If
  no candidate is a confident match, write nothing (leave it unauditable) — do not force a match.

Batch these fetches politely. See `references/lookup_api.md` for query tips and rate-limit etiquette
(add a `mailto` param to be a good citizen). For large bibliographies (50+), fetch in groups and
keep going; partial results still produce a useful report.

### 4. Run the offline analysis

```bash
python scripts/analyze_references.py rv_work/references.json --lookups rv_work/lookups -o rv_work/analysis.json
```

This normalizes each cached record, does the field-by-field fuzzy matching, assigns verdicts and a
weighted match confidence, flags retractions/preprints/missing-DOIs, runs hygiene checks, and
computes the meta-analysis. It prints the meta-analysis summary to stdout.

### 5. Add relevance scores

For each reference that has enough to judge, read `in_text.contexts` against the source's title and
abstract (the abstract is in the cached lookup / the analysis `canonical.abstract`). Assign a
0–100% relevance score and a one-line rationale, and write them into the reference's `relevance`
field in `rv_work/analysis.json`:

```json
"relevance": {"score": 78, "rationale": "Supports the stated result on X; same population and method."}
```

Guidance for scoring: 85–100 the source directly substantiates the specific claim; 60–84 topically
relevant but not a direct substantiation; 30–59 tangential; below 30 the citation looks misplaced or
the claim isn't supported. If a reference has no usable context or no metadata, leave relevance null
and say so. Keep rationales short and concrete. Remember these are advisory judgments — the report
labels them as AI-generated.

You can edit analysis.json directly (it's JSON) or re-run step 4 with relevance pre-filled in
references.json; either works since the scripts pass `relevance` through.

### 6. Generate the deliverables

```bash
python scripts/build_reports.py rv_work/analysis.json --outdir "<USER_FOLDER>" --basename "<name>_reference_audit"
```

This writes `<name>_reference_audit.docx` and `<name>_reference_audit.xlsx`. Then present both files
to the user and give a 2–3 sentence summary highlighting the headline numbers and any red flags
(broken DOIs, mismatches, retractions).

## Report contents

**Word** — title, executive summary, an "items needing attention" line, the AI-relevance disclaimer,
a meta-analysis metrics table with charts (status distribution, DOI coverage, relevance histogram),
reference-type breakdown, a citation-hygiene table, and a per-reference detail section (status
badge, DOI/source line, relevance score + rationale, flags, and a color-coded field-comparison
table — or a parsed component breakdown for unauditable items).

**Excel** — `Summary` (all meta metrics), `References` (one row per reference with every verdict,
scores, status, relevance, flags, color-coded), `FieldMatches` (long form: one row per field
comparison), `Issues` (hygiene), and `Unauditable` (every no-DOI / 404 reference with its parsed
components and the reason).

## Notes & edge cases

- **Author–year manuscripts:** ids can be like `Smith2020`; keep them stable between references.json
  and lookups filenames.
- **Off-by-one years** (online-first vs print) are scored as a Partial, not a hard mismatch.
- **Retraction detection** is best-effort from Crossref metadata (title text, `update-to`,
  `relation`). Treat a flag as "verify manually," and mention that limitation to the user.
- **Preprints:** if the cited item is a preprint that now has a published version, the report
  suggests citing the published DOI.
- **Don't fabricate matches.** If discovery is uncertain, leave the reference unauditable — a false
  "verified" is worse than an honest "couldn't confirm."
- If the user only wants a quick pass, you can skip discovery (step 3, no-DOI branch) and relevance
  (step 5); the report still covers everything else.
