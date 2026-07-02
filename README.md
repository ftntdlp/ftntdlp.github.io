# DLP Test Files

A simple, static web page for testing **Data Loss Prevention (DLP)** configurations. It provides sample files that contain synthetic sensitive data so you can verify whether your DLP tooling correctly detects and blocks them.

## What it does

The page ([index.html](index.html)) presents a clean, minimalist list of full-width rows. Each row shows a file-type tag, a title, and a brief description, and links to a test file hosted in the [`ftntdlp/dlp-test-files`](https://github.com/ftntdlp/dlp-test-files) repository.

The current set of files contain **Credit Card numbers and/or US Social Security Numbers (SSN)**:

| Tag | File | Description |
| --- | --- | --- |
| DOC | `ssn-cc.doc` | Word document embedding sample credit card and SSN values. |
| PDF | `ssn-cc.pdf` | PDF document with credit card and SSN data in its text. |
| ZIP | `ssn-cc.zip` | Compressed archive — tests detection inside packed files. |
| TXT | `ssn.txt`  | Plain text file listing sample SSN values. |
| PY  | `dlp_test_sample.py` | Python source file with sensitive data — **copies to clipboard** (no download) to test clipboard-based DLP. |

The first four rows open the raw file in a **new tab** (`window.open(..., '_blank')`). This is intentional: opening in a separate tab lets a DLP block/warning page render on its own without replacing this test site.

The **PY (Source Code)** row is different — instead of downloading, it `fetch()`es the raw file text from `raw.githubusercontent.com` and writes it to the clipboard via the Clipboard API, then shows a "Copied!" confirmation. This tests clipboard/endpoint DLP rather than file-transfer DLP. It requires a secure context (HTTPS or `localhost`), which GitHub Pages provides.

## Usage

Because it's a fully static page with no build step, you can:

- **Open locally** — open `index.html` directly in a browser, or serve the folder:
  ```sh
  python3 -m http.server 8000
  # then visit http://localhost:8000
  ```
- **Host on GitHub Pages** — the repo name (`ftntdlp.github.io`) indicates it is intended to be served as a GitHub Pages site at `https://ftntdlp.github.io`.

To test your DLP setup, click a box to download (or open) a file and confirm your DLP solution flags, quarantines, or blocks the transfer as expected.

## Structure

```
.
├── index.html   # Single self-contained page (HTML + inline CSS)
└── README.md
```

The page uses inline `<style>` for layout and inline `onclick` handlers for navigation — there are no external dependencies, scripts, or assets.

## ⚠️ Note

The linked files contain **synthetic / test data only**. They are intended for security testing and DLP validation. Do not treat the sample SSN or credit-card values as real.
