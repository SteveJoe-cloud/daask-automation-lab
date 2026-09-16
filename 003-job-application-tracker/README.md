# 003: Job Application Tracker with Assisted Auto-Fill

**Sector:** Personal (job search tooling, not a client-facing build)
**Technique:** RSS ingestion, two-pass LLM tailoring with self-critique, Google Sheets as a cross-tool data bridge, Automa browser automation, Playwright/CDP bridge for file uploads
**Built:** September 2026, ongoing
**Status:** In progress, architecture designed, Phase 1 (n8n ingestion and tailoring) specified but not yet confirmed built. The file-upload bridge (Phase 3's hardest piece) has a working proof-of-concept script pending a live test.

## Cost solved

Manual job searching: reading each JD, cross-referencing it against a resume and FAQ answers, and re-typing similar information into every application form.

## How it works (four phases)

1. **Ingestion & AI processing (n8n):** an RSS-based job alert triggers a fetch of the full JD, then two DashScope/Qwen LLM passes, one to tailor a summary and FAQ answers against a master profile, a second to self-critique the output against the original JD for missed requirements. Results land in a Job_Tracker Google Sheet.
2. **Review (AppSheet):** a mobile dashboard reads the same sheet, highlighting high-match roles, letting edits be made directly against the tailored fields before anything is submitted.
3. **Browser execution (Automa):** Automa wakes on matching ATS URLs (Greenhouse, Lever), reads the matching row from the tracker sheet, and fills the visible form fields.
4. **File upload bridge (Playwright over CDP):** since browser extensions cannot programmatically set a file input's value (a deliberate browser security restriction, not a missing setting), a small local script connects to Chrome via the DevTools Protocol and performs the resume upload at the browser-control level instead of the page level.

Every application still ends with a human reviewing the filled form and clicking submit, this was a deliberate design constraint from the start, not an unattended auto-apply bot.

## Stack

n8n, DashScope/Qwen, Google Sheets, AppSheet, Automa, Python + Playwright

## Known limitations

Full auto-apply across arbitrary ATS platforms isn't reliable, Workday in particular sometimes doesn't recognize a CDP-set file even when technically attached. This system assists and prepares, it doesn't remove the need for a final human pass.

## Demo

Not yet recorded, build still in progress.
