# Daniel Miin One-Page Site

Static personal website for `miin.ai`. The site presents Daniel Miin's profile, an AI-generated bio slide page, a founder mentoring resource, and a short write-up on the `kb.miin.ai` knowledge base.

## Site Structure

- `index.html` - main one-page profile with contact links and topic cards.
- `dan.html` - AI-generated bio slide page using images in `assets/dan-slides/`.
- `mentoring-founders.html` - health tech founder funding-readiness guide with downloadable diligence checklist and tombstone gallery.
- `kb-build.html` - overview of the `kb.miin.ai` knowledge base build.
- `assets/dan-slides/` - slide images and OCR JSON for the bio page.
- `assets/tombstones/` - transaction tombstone images used by the founder mentoring page.
- `assets/mentoring-founders/` - downloadable founder resources.
- `CNAME` - GitHub Pages custom domain configuration for `miin.ai`.

## Tech Stack

- Static HTML files with embedded CSS and vanilla JavaScript.
- Responsive card-based layouts with light/dark theme support.
- Theme preference stored with `localStorage` and shared by cookie across `miin.ai` subdomains when possible.
- Hosted as a static site, suitable for GitHub Pages.
- No package manager, build step, or runtime server is required.

## Local Preview

Open `index.html` directly in a browser, or run a small static server from the repo root:

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080`.

## Deployment

Push changes to `main`. GitHub Pages serves the static files at the custom domain listed in `CNAME`.
