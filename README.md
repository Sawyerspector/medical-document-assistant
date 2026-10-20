# 🩺 Medical Document Assistant

Local-first RAG assistant for medical documents

Medical records are scattered across patient portals, hospital systems, lab and imaging portals, and pharmacies, which makes them messy and hard to find. Medical Document Assistant brings them together in one place and lets **clinicians and patients ask questions about them in plain language**, with every answer **cited back to the source document and page**.

Today, users upload records they've exported or downloaded. Importing directly from portals and health systems is on the roadmap. Everything runs on the user's own machine by default, and no patient data is sent anywhere unless a remote model is explicitly configured.

Built solo and refined with feedback from healthcare professionals. Currently awaiting server integration to run AI locally inside a clinic.

> **Note:** This is a showcase repository. The source code is private while the project is in active development — available on request.

<!-- Add a screenshot of a cited answer here: drag an image into the GitHub editor -->

---

## How It Works

**Upload → Parse → Chunk & Embed → Retrieve → Cited Answer**

1. **Upload:** PDF, DOCX, TXT, and Markdown files, with duplicate detection and size limits
2. **Parse:** text extraction with an explicit status for every file (parsed, empty, needs OCR, failed), so problem files never disappear silently
3. **Chunk & embed:** page-aware chunking and CPU embedding into a local ChromaDB index
4. **Retrieve:** a calibrated distance cutoff drops unrelated chunks before they reach the LLM
5. **Answer:** a local model (Currently Llama 3.1 8B) generates the answer, and citation markers are validated against the retrieved sources. If the answer isn't in the documents, it says so instead of guessing.

---

## Key Features

- **Clinician and patient modes** that adjust answer language to the reader
- **Clickable citations** with side-by-side source viewing
- **Cited document summaries**, grounded in the document's own text and cached by content hash
- **Query decomposition** for complex questions, with a single-shot fallback
- **Scope-aware suggested questions**, filtered so weak suggestions aren't shown
- **Clinician schedule** with per-patient chart-readiness warnings and one-click visit prep
- **Document browser** with filtering, sorting, metadata editing, and reindex recovery
- **Swappable LLM backend:** any OpenAI-compatible endpoint, defaulting to local Ollama

---

## Evaluation & Testing

- Synthetic QA evaluation suite covering **retrieval hits, citation source matching, document scoping, and not-found behavior**
- Test suite with **pytest**, run against a throwaway temp database using only synthetic data

---

## Privacy by Design

- Runs entirely on the user's machine; remote LLM use is **off by default**
- Logs contain only document IDs, counts, and error types — never filenames, document text, or prompts
- Planned integrations (OCR, C-CDA, FHIR) are labeled "planned" in the UI, never simulated

---

## Tech Stack

**Backend:** Python, FastAPI, ChromaDB, Ollama (Llama 3.1 8B)
**Frontend:** React, Vite, TypeScript
**Testing:** pytest

---

## Roadmap

- Local OCR for scanned documents
- Structured import of patient portal exports (C-CDA/CCD)
- FHIR / SMART on FHIR retrieval, behind real authentication and a security review
- Real authentication, verified roles, and audit events
- Server deployment for local AI use inside a clinic

---

**Demonstrated Skills:** Retrieval-Augmented Generation, LLM Evaluation, Information Retrieval, Full-Stack Development, Privacy-First System Design, Testing
