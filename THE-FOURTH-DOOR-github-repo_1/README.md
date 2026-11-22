# The Fourth Door, website

Single-page site, Build 14.4. No build step, no framework. Open `index.html` in a browser and it works.
GitHub Pages deploys this folder on every push to `main` (see `.github/workflows/pages.yml`).

```
index.html            the entire site: markup, CSS and JS in one file
assets/
  lee.jpg             portrait, first screen
  pete.jpg            portrait, first screen
  guide-cover.jpg     the 20 Checks cover
og-image.png          1200x630 social share card, must sit at the root
the-20-checks.pdf     the 28-page guide
_redirects            pretty URLs, only read by Netlify
CNAME                 thefourthdoor.co.uk, needed by GitHub Pages
```

## Before this build is fully live (search index.html for TODO)

1. Forms. All three forms (calculator, 20 Checks, application) have `data-endpoint=""`. Paste a Formspree form URL into each. Until then nothing is sent or stored, and the page says so quietly after submit.
2. Footer and Apply panels. Phone number, WhatsApp number, company number and registered address are placeholders.
3. Video. A commented-out block in the Two Builders section takes `assets/lee-and-pete.mp4` when the footage exists.
4. Photos. The bios run without photographs until two more portraits exist; the first-screen portraits are not reused.

## Rules that have already saved this site once

- Objects may move; words hold still. No animation ever touches a sentence.
- A highlight owns its line. Every lime-highlighted phrase starts flush on its own line.
- Credentials follow tenfoldpartners.co.uk word for word (nine-figure valuation, 150 businesses scaled, 65+ acquisitions, 2,500-person organisation, 200 leaders coached). Do not reintroduce older figures.
- Photography or nothing. No stock, no generated faces.
- Verify in a browser before shipping. Chromium at 1440 and 390, console clean.

## Motion

GSAP 3.12.5 and ScrollTrigger from cdnjs drive the pinned "Years" track. Everything else is CSS. Reduced motion and no-JS both render in full; the folds are native `details` elements.
