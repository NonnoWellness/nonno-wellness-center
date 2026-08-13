# Nonno Wellness Center — Website

Static HTML/CSS/JS website. No build step, no framework, no dependencies — deploy the folder as-is to any static host. Internal links use root-relative paths (e.g. `/assets/site.css`), so a local web server is needed for preview (see "Local Preview" below) and the site must be deployed at the domain root.

## File Structure

```
index.html                     ← Homepage
assets/
  site.css                     ← Shared stylesheet used by all program/area pages
  nonno-logo.png                ← Site logo (used in header/footer, transparent PNG)
  favicon-16.png, favicon-32.png, apple-touch-icon.png
  iop-group-room.jpg           ← Lounge/group room photo, IOP page
  iop-group-room-2.jpg         ← Second lounge area photo, IOP page
  iop-meeting-room.jpg         ← Conference room photo, IOP page
  sober-living-house.jpg       ← Exterior photo, Sober Living page
programs/
  iop.html
  sober-living.html
  ulsa.html
areas/
  redondo-beach.html
  hermosa-beach.html
  manhattan-beach.html
  palos-verdes.html
  san-pedro.html
  torrance.html
  el-segundo.html
  greater-los-angeles.html
robots.txt
sitemap.xml
```

**Important:** the homepage (`index.html`) uses its own inline `<style>` block. All pages inside `programs/` and `areas/` link out to the shared `assets/site.css` instead — this keeps the design consistent and means style changes only need to happen in one place. Do not delete or move `assets/site.css`, or every program and area page will lose all styling.

## Before Deploying

1. **Homepage is named `index.html`, and all internal links are root-relative** (e.g. `href="/programs/iop.html"`, not a relative path) — this was changed after relative paths broke on a live deploy, likely from the host rewriting URLs. Root-relative paths only resolve correctly if the site is deployed at the domain root — see "Local Preview" below for why this also changes local testing.

2. **Update canonical URLs and schema** — every page has a `<link rel="canonical">` tag and `og:url` meta tag pointing to `https://www.nonnorecovery.com/...`. If the final live URL structure differs (e.g. program pages live at a different path), these need to be updated to match, along with the JSON-LD structured data (`<script type="application/ld+json">`) on each page.

3. **Google Analytics 4** — already wired up with the real Measurement ID (`G-HQK2T4GJDB`) on all 12 pages. No action needed unless this property changes.

4. **San Pedro ILWU sober living home** — the San Pedro area page and the ULSA program page both reference a sober living home located directly in San Pedro, exclusively for ILWU members. No street address is included yet since one hasn't been provided — add one (and update the JSON-LD schema on both pages to reflect it as a second business location) if/when available.

5. **Insurance verification form** — the form on the homepage submits via Formspree to `info@nonnowellness.com`. It's already live and tested. No changes needed unless you want to move it to a different form backend.

6. **Insurance carrier badges** — the "we accept" section currently shows carrier names as styled text badges, not official logos. Swap in real logo files if/when they're available.

## Local Preview

**This site now uses root-relative paths** (e.g. `/assets/site.css`, `/programs/iop.html`) instead of relative paths, because relative paths broke on the live server — likely due to the host normalizing URLs (stripping `.html`, adding trailing slashes), which changes how the browser resolves `../` paths. Root-relative paths are immune to that and are the standard approach for real deployments — but it means:

- **You can no longer just double-click `index.html` to preview it** — opening it directly via `file://` won't resolve `/assets/...` correctly, since there's no server to anchor "/" to.
- **To preview locally, run a simple local server** from this folder and open it via `http://localhost`:
  ```
  python3 -m http.server 8000
  ```
  then visit `http://localhost:8000` in a browser.
- **On the live server, the site must be deployed at the domain root** (`https://www.nonnorecovery.com/`, not a subdirectory like `https://www.nonnorecovery.com/site/`) — since `/assets/...` resolves from whatever domain root the browser is on. If this ever needs to live in a subdirectory instead, every root-relative path across all 12 files would need a matching prefix added.

## Deployment Notes

Since this is a fully static site, it's compatible with any static hosting provider (GitHub Pages, Netlify, Vercel, Cloudflare Pages, S3 + CloudFront, or a traditional web host via FTP/SFTP). No server-side language, database, or build pipeline is required.
