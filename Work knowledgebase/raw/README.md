# raw/ — Immutable sources

This is your **source of truth**. Drop source documents in here and they stay
exactly as they are — the LLM reads from them but never edits them.

Subfolders:

- `articles/` — web clippings, blog posts (markdown or `.txt`)
- `papers/` — PDFs, research papers, reports
- `notes/` — meeting notes, transcripts, your own raw notes
- `data/` — CSVs, spreadsheets, datasets
- `assets/` — images referenced by the above

## How to add a source

1. Save the file into the right subfolder.
2. Tell the LLM: *"ingest raw/articles/<filename>"*.
3. The LLM reads it, writes a summary into `wiki/sources/`, updates the relevant
   entity and concept pages, and logs the ingest.

Nothing here should ever be hand-edited after the fact. If a source changes,
add the new version as a new file so the history stays intact.
