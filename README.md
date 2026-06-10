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

- Local repo: `/Volumes/Acer Dock SSD/Knowledge-Site`
- GitHub remote: `git@github.com:danmiinai/miinai-knowledge-base.git`
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

## Local Preview

Open any HTML file directly in a browser, or run a small static server from the repo root:

```bash
python3 -m http.server 8080
```

Then visit <http://localhost:8080>.

Useful local URLs:

- <http://localhost:8080/index.html>
- <http://localhost:8080/kb-build.html>
- <http://localhost:8080/apple-intelligence.html>

## Validation

Before pushing HTML edits, run:

```bash
tidy -qe index.html
tidy -qe kb-build.html
tidy -qe apple-intelligence.html
git diff --check
```

Run `tidy -qe` on any other edited HTML page as needed.

## Deployment

### `miin.ai`

Push changes in this repo to `main`:

```bash
git status --short --branch
git add <changed-files>
git commit -m "Describe the site update"
git push origin main
```

GitHub Pages should publish automatically. If the custom domain stops resolving, check that the Pages custom domain is still set to `miin.ai` and that the domain remains verified for the GitHub organization.

### `kb.miin.ai`

Deploy the knowledge app from `/Volumes/Acer Dock SSD/Knowledge-Site`, not from this static-site repo.

The app uses Firebase App Hosting. `apphosting.yaml` configures a low-cost runtime with `minInstances: 0`, `maxInstances: 2`, `concurrency: 80`, and `memoryMiB: 2048`.

Required App Hosting secrets:

```bash
firebase apphosting:secrets:set gemini-api-key
firebase apphosting:secrets:set google-drive-folder-id
```

Useful app checks before deploying:

```bash
npm run lint
npm run typecheck
npm run build
```

Content indexing is intentionally separate from deploys. Ongoing Drive sync should normally run locally:

```bash
npm run sync:drive
SYNC_ONLY_MISSING=1 npm run sync:drive
```

Production remote sync is disabled unless `ENABLE_REMOTE_SYNC=1` is explicitly set.
