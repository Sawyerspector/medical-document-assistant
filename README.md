# 🩺 Medical Document Assistant

Local-first RAG assistant for medical documents

Medical records are scattered across patient portals, hospital systems, lab and imaging portals, and pharmacies, which makes them messy and hard to find. Medical Document Assistant brings them together in one place and lets **clinicians and patients ask questions about them in plain language**, with every answer **cited back to the source document and page**.

Today, users upload records they've exported or downloaded. The goal is to pull records directly from where they already live, such as EHR systems like Epic and existing patient portals, so no one has to collect them by hand. Everything runs on the user's own machine by default, and no patient data is sent anywhere unless a remote model is explicitly configured.

Built solo and refined with feedback from healthcare professionals. Currently awaiting server integration to run AI locally inside a clinic.

> **Note:** This is a showcase repository. The source code is private while the project is in active development and is available on request. All patient data shown is synthetic.

---

## Walkthrough: A Clinician's Day

### 1. Start with the schedule
The day opens on the clinician's schedule. Each visit shows how many records are on file, and charts that may be out of date are flagged before the patient arrives, like the warning that Elena Petrova's newest record is over 180 days old.

<p align="center">
  <img width="100%" alt="Clinician schedule showing today's visits, document counts, and a chart-readiness warning" src="https://github.com/user-attachments/assets/ea9ea84a-aa6e-44ef-bf01-27e176d30005" />
</p>

### 2. Open the patient's chart
Clicking **Prepare** opens the chart. Uploaded records are sorted into summaries, labs, imaging, and medications, alongside the patient's visit history and next appointment.

<p align="center">
  <img width="100%" alt="Patient chart overview with records organized by type and visit history" src="https://github.com/user-attachments/assets/9af8d1fb-9d20-43e6-8c7d-7bb80858351f" />
</p>

### 3. Review what's changed
The visit-prep brief summarizes everything new since the last visit: new lab results, a medication added, and overdue follow-ups. Every point is cited, and the source documents are listed underneath.

<p align="center">
  <img width="100%" alt="Visit-prep brief listing new labs, medication changes, and follow-ups, each with a citation" src="https://github.com/user-attachments/assets/8eb8bf40-be26-4429-95dd-f54f517cfb3a" />
</p>

### 4. Ask a specific question
For anything more specific, the clinician asks in plain language. Here, the assistant tracks a patient's creatinine across two lab reports, cites the exact document and page for each value, and suggests relevant follow-up questions.

<p align="center">
  <img width="100%" alt="Ask page answering a question about creatinine trends with cited lab reports" src="https://github.com/user-attachments/assets/7a301234-11da-4cb8-b74f-61684b25dadf" />
</p>

---

## How It Works

**Upload → Parse → Chunk & Embed → Retrieve → Cited Answer**

1. **Upload:** PDF, DOCX, TXT, and Markdown files, with duplicate detection and size limits
2. **Parse:** text extraction with an explicit status for every file (parsed, empty, needs OCR, failed), so problem files never disappear silently
3. **Chunk & embed:** page-aware chunking and CPU embedding into a local ChromaDB index
4. **Retrieve:** a calibrated distance cutoff drops unrelated chunks before they reach the LLM
5. **Answer:** a local model (currently Llama 3.1 8B) generates the answer, and citation markers are validated against the retrieved sources. If the answer isn't in the documents, it says so instead of guessing.

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

**Backend:** Python, FastAPI, ChromaDB, Ollama (Llama 3.1 8B)<br />
**Frontend:** React, Vite, TypeScript<br />
**Testing:** pytest

---

## Roadmap

- Local OCR for scanned documents
- Structured import of patient portal exports (C-CDA/CCD)
- Direct, patient-authorized retrieval from EHR systems such as Epic and from existing patient portals via FHIR / SMART on FHIR, behind real authentication and a security review
- Schedule sync with EHR and practice-management systems
- Real authentication, verified roles, and audit events
- Server deployment for local AI use inside a clinic

---

**Demonstrated Skills:** Retrieval-Augmented Generation, LLM Evaluation, Information Retrieval, Full-Stack Development, Privacy-First System Design, Testing
