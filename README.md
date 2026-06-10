# miin.ai Website

Static personal website for `miin.ai`. This repo owns the public profile site, selected AI build notes, founder mentoring materials, and supporting media. The related `kb.miin.ai` knowledge search app is documented here, but its application code lives in a separate local repo.

## Live Sites

- Main site: <https://miin.ai/>
- Knowledge search app: <https://kb.miin.ai/>
- Knowledge base build note: <https://miin.ai/kb-build.html>
- Apple Intelligence build note: <https://miin.ai/apple-intelligence.html>

GitHub Pages serves this static site from `main` using the custom domain in `CNAME`.

## Site Structure

### This Repo: `miin.ai`

- `index.html` - main profile page with contact links and topic cards.
- `dan.html` - AI-generated bio slide page using images and OCR metadata in `assets/dan-slides/`.
- `mentoring-founders.html` - health tech founder funding-readiness guide with a downloadable diligence checklist and transaction tombstone gallery.
- `kb-build.html` - white paper on building `kb.miin.ai`, including the current Firebase-backed architecture and earlier Vercel/Supabase tradeoffs.
- `apple-intelligence.html` - white paper on building Intelligent AI Pip for Corebound with local iOS game intelligence and Apple Intelligence as an editorial layer.
- `assets/dan-slides/` - slide images and OCR JSON for the bio page.
- `assets/tombstones/` - transaction tombstone images used by the founder mentoring page.
- `assets/mentoring-founders/` - downloadable founder resources, including the representative diligence checklist.
- `CNAME` - GitHub Pages custom domain configuration for `miin.ai`.

### Companion App: `kb.miin.ai`

- Purpose: a Google-style knowledge search app that retrieves private Google Workspace content from Cloud Firestore vector search and answers with Gemini.
- Public relationship to this repo: `kb-build.html` documents the build and links out to the live app at `https://kb.miin.ai/`.

## Tech Stack

### `miin.ai`

- Static HTML files with embedded CSS and vanilla JavaScript.
- Responsive card-based layouts with light/dark theme support.
- Theme preference stored in `localStorage` and shared by cookie across `miin.ai` subdomains when possible.
- Hosted on GitHub Pages with no package manager, build step, or runtime server.

### `kb.miin.ai`

- Next.js App Router with TypeScript and React.
- Firebase App Hosting for the deployed web app.
- Cloud Firestore Native mode with vector search for source and chunk retrieval.
- Gemini chat model: `gemini-2.5-flash`.
- Gemini embedding model: `gemini-embedding-001` at 768 dimensions.
- Google Drive API ingestion from a Workspace folder.
- Excel parsing for Google Sheets and `.xlsx`/`.xlsm` files.
- Image OCR for common image formats through Tesseract.js.
- Local sync flow uses Application Default Credentials and writes indexed content to Firestore.
