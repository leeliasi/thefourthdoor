# The Fourth Door — website

Single-page site. No build step, no framework, no package manager. Open `index.html` in a browser and it works.

```
index.html            the entire site: markup, CSS and JS in one file
assets/
  lee-liasi.jpg       portrait, used in the two-builders section
  pete-taylor.jpg     portrait, used in the two-builders section
  guide-cover.jpg     the book cover shown next to the download form
og-image.png          1200x630 social share card, must sit at the root
the-20-checks.pdf     the 28-page guide
_redirects            pretty URLs, only read by Netlify
```

Deploy by uploading the whole folder. Nothing needs compiling.

---

## Read this before editing

Five things in here have already broken once. Each has a rule.

**1. Any heading with a lime highlight needs room.**
The `.hl` class paints a lime block behind inline text. At the display line-height the block collides with the line above and covers it. There is a safety rule near the top of the stylesheet:

```css
:where(h1,h2,h3):has(.hl){line-height:1.22}
```

Do not remove it. If you add a highlighted heading, give it `class="bigclaim"` or leave the safety rule to catch it.

**2. The navigation must stay on one row.**
Six items is the maximum at the current sizes. `.navlinks` is set to `flex-wrap:nowrap` deliberately, so a seventh item will visibly break rather than silently restack onto a second row, which is what happened before. If you add an item, remove one.

**3. The hero must fit one screen.**
`.hero h1` is sized `clamp(34px, min(11vw,14vh), 168px)` — width **and** height. Removing the `vh` term makes the headline enormous on a laptop and pushes the buttons off the bottom of the screen. Each headline phrase is also `white-space:nowrap`, because when a phrase wraps onto two lines the hero doubles in height.

**4. Form fields need a `name` attribute or they transmit nothing.**
`FormData` only collects named fields. The application form silently dropped the applicant's name, business and answer for several builds because they had `id` but no `name`.

**5. Both forms refuse to submit until an endpoint is set.**
Each carries `data-endpoint=""`. While empty, submitting prints a message and sends nothing, by design, so a lead can never vanish quietly. To go live, put the endpoint URL in that attribute on both forms.

---

## Preview-only, remove before launch

Three things are marked in the file with `PREVIEW ONLY` comments:

1. `<meta name="robots" content="noindex, nofollow">` — keeps the test copy out of Google so it never competes with the real domain
2. The **"Read it now, no email"** button beside the book — lets reviewers read the guide without a working form. On the live site the email address *is* the point, so this must go
3. The preview wording in the form guard — harmless, and stops firing on its own once an endpoint is set

The social tags currently point at `https://leeliasi.com/`. Change `og:url` and both image tags to the real domain at launch, and restore the canonical link.

---

## Still outstanding

- Form endpoint on both forms, or nothing is captured
- Real company details in the footer, currently test data
- Real telephone number: `020 7946 0100` is an Ofcom drama-range placeholder, deliberately not a real number
- A privacy notice page at `/privacy`
- Pete Taylor has not yet reviewed his own bio, role label or portrait

---

## The calculator

Lives in `#worth`. Pure client-side arithmetic, no backend. The model is:

**multiple = sector band, scaled by business size, positioned by readiness score.**

Sector bands are set as `data-lo` and `data-hi` on each `.sec` tile. Size scales the whole band: 0.60 under £250k of adjusted EBITDA, rising to 1.08 above £5m. The five founder checks count double, giving a weighted score out of 25. Output is always a range, never a single figure.

If you change the bands, keep them inside published UK data. The first version returned 14.9x for a small software business, which is not a number anybody would pay.
