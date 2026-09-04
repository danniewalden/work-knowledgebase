---
source_url: https://simonwillison.net/2026/Sep/1/codex-libreoffice/
title: Codex bundles LibreOffice
author: Simon Willison
publication: Simon Willison's Weblog
published: 2026-09-01
retrieved: 2026-09-02
type: article
---

# Codex bundles LibreOffice

I was poking around in my `~/.cache/` folder using [OmniDiskSweeper](https://www.omnigroup.com/more) when I spotted something interesting. The OpenAI Codex desktop app (since [rebranded](https://help.openai.com/en/articles/20001276-moving-to-the-new-chatgpt-desktop-app) to just ChatGPT) has 1.7GB of stuff in there in a folder called `codex-primary-runtime`, including a full Python installation, a full Node.js installation, and native binaries for [Poppler](https://poppler.freedesktop.org), git, and the [LibreOffice](https://en.wikipedia.org/wiki/LibreOffice) open source office suite (which forked from OpenOffice.org in 2010):

*[Image: Screenshot of a macOS disk usage app window in column view, titled "/Users/simon/.cache - 442.1 GB". First column: 356.8 GB huggingface, 82.5 GB uv, 1.7 GB codex-runtimes (selected), 609.0 MB datasette-sqlite, 298.8 MB rod. Second column: 1.7 GB codex-primary-runtime (selected). Third column: 1.7 GB dependencies (selected), 6.3 MB plugins, 4.1 kB runtime.json. Fourth column: 771.0 MB native (selected), 446.4 MB node, 440.6 MB python, 28.7 kB bin. Fifth column: 429.7 MB libreoffice-headless (selected), 187.9 MB poppler, 148.1 MB git, 4.7 MB libheif, 679.9 kB jxrlib.]*

The `~/.cache/codex-runtimes/codex-primary-runtime/plugins/openai-primary-runtime/plugins/documents` folder includes skills which tell Codex how to find and use those binaries.

Tags: codex, generative-ai, openai, ai, llms, openoffice, open-source

## Capture note (not part of the source)

Captured from the full-content Atom feed at simonwillison.net/atom/everything/; HTML entities decoded and markup converted to Markdown.
