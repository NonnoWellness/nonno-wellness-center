# Nonno Wellness Center — Website

Static HTML/CSS/JS website. No build step, no framework, no dependencies — every page can be opened directly in a browser or deployed as-is to any static host.

## File Structure

```
nonno-recovery-redesign.html   ← Homepage
assets/
  site.css                     ← Shared stylesheet used by all program/area pages
  nonno-logo.png                ← Site logo (used in header/footer, transparent PNG)
  favicon-16.png, favicon-32.png, apple-touch-icon.png
  iop-group-room.jpg           ← Photo used on the IOP program page
  sober-living-house.jpg       ← Photo used on the Sober Living program page
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

**Important:** the homepage (`nonno-recovery-redesign.html`) uses its own inline `<style>` block. All pages inside `programs/` and `areas/` link out to the shared `assets/site.css` instead — this keeps the design consistent and means style changes only need to happen in one place. Do not delete or move `assets/site.css`, or every program and area page will lose all styling.

## Before Deploying

1. **Rename the homepage file** — `nonno-recovery-redesign.html` should become `index.html` (or your host's expected entry-point filename) before going live. All internal links reference the homepage by relative path with anchors (e.g. `../nonno-recovery-redesign.html#verify-insurance`), so if you rename it, do a find-and-replace across every file in `programs/` and `areas/` for `nonno-recovery-redesign.html` → `index.html` (or whatever you rename it to).

2. **Update canonical URLs and schema** — every page has a `<link rel="canonical">` tag and `og:url` meta tag pointing to `https://www.nonnorecovery.com/...`. If the final live URL structure differs (e.g. program pages live at a different path), these need to be updated to match, along with the JSON-LD structured data (`<script type="application/ld+json">`) on each page.

3. **Add the real Google Analytics 4 Measurement ID** — every page currently has a GA4 snippet with a placeholder ID (`G-XXXXXXXXXX`). Find-and-replace that string across all files with the real Measurement ID once you have one.

4. **Insurance verification form** — the form on the homepage submits via Formspree to `info@nonnowellness.com`. It's already live and tested. No changes needed unless you want to move it to a different form backend.

5. **Insurance carrier badges** — the "we accept" section currently shows carrier names as styled text badges, not official logos. Swap in real logo files if/when they're available.

## Local Preview

No server or build step required — just open `nonno-recovery-redesign.html` directly in a browser. Internal links between pages use relative paths, so the whole folder structure needs to stay together (don't move `programs/` or `areas/` files out on their own).

## Deployment Notes

Since this is a fully static site, it's compatible with any static hosting provider (GitHub Pages, Netlify, Vercel, Cloudflare Pages, S3 + CloudFront, or a traditional web host via FTP/SFTP). No server-side language, database, or build pipeline is required.
