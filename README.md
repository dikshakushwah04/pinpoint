# Pinpoint

**Document intelligence, without the data leaving your browser.**

Pinpoint is a client-side document Q&A tool. Upload PDFs and Word docs, ask questions in plain English, and get answers grounded in your files — with inline citations pointing back to the exact source document and excerpt.

🔗 **[Try it live](https://dikshakushwah04.github.io/pinpoint/)** *(enable GitHub Pages in repo settings to activate this link)*

## Why Pinpoint

Most document Q&A tools require uploading files to a third-party server. Pinpoint doesn't. Everything — PDF parsing, Word doc extraction, chunking, and search — happens entirely in the browser. The only network call is the actual question sent to the LLM, and only the relevant document text goes with it. Your files and your API key never touch a backend, because there isn't one.

## Features

- **Multi-format ingestion** — drag-and-drop PDFs (via [pdf.js](https://mozilla.github.io/pdf.js/)) and Word docs (via [Mammoth.js](https://github.com/mwilliamson/mammoth.js))
- **Grounded answers with citations** — every response cites the specific document and excerpt it was based on, so you can verify claims instead of trusting a black box
- **Smart context windowing** — long documents are automatically chunked and the most relevant sections are selected before hitting the token budget, so answers stay accurate even across large files
- **Scoped search** — ask questions across all uploaded documents at once, or narrow to a single file
- **Persistent history** — past Q&A sessions are saved locally, searchable and taggable, so you can revisit earlier findings
- **Rate-limit resilient** — automatically detects and retries on API rate limits with a visible countdown, instead of just failing
- **Zero backend** — a single HTML file. No server, no database, no build step.

## Tech stack

| Layer | Tool |
|---|---|
| PDF parsing | pdf.js |
| Word doc parsing | Mammoth.js |
| LLM inference | [Groq API](https://groq.com/) (Llama 3.3 70B) |
| Storage | Browser `localStorage` |
| UI | Vanilla HTML/CSS/JS — no framework, no dependencies to install |

## Getting started

1. Clone this repo or download `index.html`
2. Open `index.html` in any modern browser (or serve it via GitHub Pages)
3. Enter your [Groq API key](https://console.groq.com/keys) when prompted — it's stored only in your browser's local storage
4. Upload a document and start asking questions

No installation, no build process, no server setup required.

## How it works

1. Documents are parsed client-side into raw text
2. On each question, Pinpoint scores document chunks for relevance to the query and selects the most useful sections within a token budget
3. The selected context is sent to Groq's API along with the question, with instructions to answer strictly from the provided text and cite sources
4. The response — including citations and auto-generated tags — is parsed, displayed, and saved to local history

## Privacy

Pinpoint was built with a privacy-first design: documents are processed and stored entirely client-side. Nothing is uploaded to any server except the minimal text context sent directly to the Groq API for answering a question.

## About

Built by [Diksha Kushwah](https://github.com/dikshakushwah04) in partnership with the Florida Bulldog nonprofit, exploring practical, privacy-conscious applications of LLMs for document-heavy workflows like journalism and research.
