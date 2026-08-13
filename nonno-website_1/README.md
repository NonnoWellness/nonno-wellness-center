# Nonno Wellness Center — Website

Static HTML/CSS/JS website. No build step, no framework, no dependencies — every page can be opened directly in a browser or deployed as-is to any static host.

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

1. **Homepage is already named `index.html`** — every internal link across all 12 pages already points to `index.html`, so this is deployment-ready as-is. **Do not rename this file** without also updating every `href="../index.html#..."` reference in `programs/` and `areas/` — if the homepage gets renamed on the server without updating those links, every header/nav link on every other page will break. (This actually happened on a previous deploy — that's why this section exists.)

2. **Update canonical URLs and schema** — every page has a `<link rel="canonical">` tag and `og:url` meta tag pointing to `https://www.nonnorecovery.com/...`. If the final live URL structure differs (e.g. program pages live at a different path), these need to be updated to match, along with the JSON-LD structured data (`<script type="application/ld+json">`) on each page.

3. **Google Analytics 4** — already wired up with the real Measurement ID (`G-HQK2T4GJDB`) on all 12 pages. No action needed unless this property changes.

4. **San Pedro ILWU sober living home** — the San Pedro area page and the ULSA program page both reference a sober living home located directly in San Pedro, exclusively for ILWU members. No street address is included yet since one hasn't been provided — add one (and update the JSON-LD schema on both pages to reflect it as a second business location) if/when available.

5. **Insurance verification form** — the form on the homepage submits via Formspree to `info@nonnowellness.com`. It's already live and tested. No changes needed unless you want to move it to a different form backend.

6. **Insurance carrier badges** — the "we accept" section currently shows carrier names as styled text badges, not official logos. Swap in real logo files if/when they're available.

## Local Preview

No server or build step required — just open `index.html` directly in a browser. Internal links between pages use relative paths, so the whole folder structure needs to stay together (don't move `programs/` or `areas/` files out on their own).

## Deployment Notes

Since this is a fully static site, it's compatible with any static hosting provider (GitHub Pages, Netlify, Vercel, Cloudflare Pages, S3 + CloudFront, or a traditional web host via FTP/SFTP). No server-side language, database, or build pipeline is required.
