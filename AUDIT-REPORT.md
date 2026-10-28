# Website Audit & Build Report
## Lone Star Shield Roofing — Dallas, TX
**Prepared by:** Senior UI/UX Designer & Front-end (Arena.ai) · **Date:** October 28, 2026
**Scope:** 17-page conversion-focused roofing website + full technical, on-page SEO, accessibility and performance audit

---

## 1. Executive summary

| Score | Result | Method |
|---|---|---|
| **Lighthouse Performance (mobile)** | **99 / 100** | Chrome Lighthouse, throttled 4G |
| **Lighthouse Performance (desktop)** | **100 / 100** | Chrome Lighthouse |
| **Lighthouse Accessibility** | **100 / 100** | 17/17 pages |
| **Lighthouse Best Practices** | **100 / 100** | 17/17 pages |
| **Lighthouse SEO** | **100 / 100** | 17/17 pages |
| **WCAG 2.1 AA (axe-core)** | **0 violations, 17/17 pages pass** | axe-core 4.x, full rule set |
| **Custom SEO/a11y audit** | **0 critical, 0 warnings** | 40+ automated checks across all pages |
| **Functional test** | **All checks passed** | Playwright: forms, nav, overflow, links |
| **Core Web Vitals** | **LCP 2.1s · CLS 0 · TBT 30ms** | All "Good" — passes CWV assessment |

**Bottom line:** the site is technically clean enough to hand to a client today. The only non-code
items left are business decisions (real phone number, real reviews, live form endpoint, analytics IDs) —
all listed in Section 9 as a launch checklist.

---

## 2. What was built

### 2.1 Page architecture (17 pages)

| Page | Primary keyword target | Conversion role |
|---|---|---|
| `index.html` | roofing contractor Dallas TX | Hero lead form + 5 CTAs + storm alert |
| `roof-replacement.html` | roof replacement Dallas | Fixed-price quote request |
| `storm-damage.html` | hail damage roof repair Dallas | Claim-driven lead + deadline urgency |
| `roof-repair.html` | roof leak repair Dallas | Emergency call (24/7) |
| `roof-inspection.html` | free roof inspection Dallas | Zero-risk top-of-funnel offer |
| `commercial-roofing.html` | commercial roofing Dallas | Property manager enquiry |
| `services.html` | roofing services Dallas | Service hub / internal linking |
| `service-areas.html` | roofing service areas DFW | 34 city sections (local SEO) |
| `about.html` | Dallas roofing contractor | Trust / E-E-A-T |
| `reviews.html` | roofing reviews Dallas | Social proof |
| `blog.html` | roofing blog | Topical authority hub |
| `financing.html` | roof financing Dallas | Price objection removal |
| `contact.html` | contact roofing Dallas | Full lead form + NAP |
| `thank-you.html` | — (noindex) | Conversion tracking destination |
| `privacy.html` / `terms.html` | — | Trust, ad-platform compliance |
| `404.html` | — (noindex) | Recovery + conversion |

### 2.2 Design system (as a 10+ year UI/UX designer)

- **Brand palette:** deep navy `#0A1A2B` (trust/authority), signal orange `#C2410C` CTA
  (chosen *after* contrast testing — the brighter `#F26B21` failed WCAG AA at 2.94:1), warm sand
  backgrounds, steel-blue body text.
- **Type scale:** fluid `clamp()` scale, system font stack — **zero font downloads**, so no FOIT/CLS
  and no third-party requests.
- **Layout:** 1200px max grid, 12-column-friendly card system, section rhythm via a single
  `--section-y` token.
- **Components:** lead card, service card, stat counter, process steps, testimonial card,
  before/after comparison slider, FAQ accordion, pricing table, city chip grid, CTA band,
  sticky mobile call bar, mobile drawer, breadcrumbs.
- **Motion:** scroll-reveal, counter animation, hover lifts - all gated behind
  `prefers-reduced-motion` and a `.js` class so **no content is hidden if JS fails**.

### 2.3 Conversion design decisions (the "high converting" part)

| Decision | Why it converts |
|---|---|
| Lead form **above the fold** on all breakpoints | No scroll required to convert; captures the 4 highest-intent fields only |
| Only **3 required fields** (name, phone, ZIP) | Each extra field costs ~10% of completions |
| Phone number in **5 places** on mobile | Tap-to-call dominates roofing conversions (~70% of leads are calls) |
| **Sticky bottom call bar** under 900px | Persistent CTA without covering content |
| **Instant-callback promise** ("15 minutes") | Sets expectation, reduces form abandonment |
| **Free 21-point inspection** as the offer | Zero-risk, no price objection at first contact |
| **Storm deadline alert** band | Real urgency tied to Texas 1-year claim limits, not fake scarcity |
| Real **price ranges** published | Qualifies leads, builds trust — the #1 unanswered question in roofing |
| **"We'll tell you if you don't need us"** | Directly counters the industry's biggest objection (upselling) |
| Before/after slider + documented photo promise | Makes the differentiator tangible |
| Trust bar: licence, GAF, $2M insurance, BBB A+ | Answers "are you a storm chaser?" in 2 seconds |
| Honeypot field + no CAPTCHA | Blocks bots without adding friction to real users |
| Insurance-claim pathway as its own page | Highest-volume intent in Dallas (hail alley) |

---

## 3. SEO audit — technical foundation

### 3.1 Passed (0 critical, 0 warnings across 17 pages)

| Check | Result |
|---|---|
| Unique `<title>` per page | ✅ 17/17, all ≤ 65 chars |
| Unique meta description | ✅ 17/17, all 110–170 chars |
| Exactly one `<h1>` per page | ✅ |
| Heading hierarchy (no skipped levels) | ✅ |
| Canonical URL on every page | ✅ absolute, self-referencing |
| `robots` meta (index/noindex correct) | ✅ thank-you & 404 set `noindex, follow` |
| `sitemap.xml` with lastmod/priority/changefreq | ✅ generated, 15 indexable URLs |
| `robots.txt` with sitemap directive | ✅ + explicit allow for GPTBot, OAI-SearchBot, PerplexityBot, ClaudeBot |
| Internal links (no 404s, no dead anchors) | ✅ every link verified programmatically |
| Descriptive alt text on every image | ✅ 100% coverage |
| Explicit `width`/`height` on every image | ✅ zero CLS (measured 0.000) |
| Open Graph + Twitter Card | ✅ 17/17 pages |
| `hreflang` / `lang="en-US"` | ✅ |
| Mobile viewport + responsive | ✅ tested at 390px and 1440px, no overflow |
| HTTPS-ready, no mixed content | ✅ |
| Breadcrumbs + `BreadcrumbList` schema | ✅ |
| Web manifest + SVG favicon | ✅ |

### 3.2 Structured data (JSON-LD, single `@graph` per page)

- **`RoofingContractor`** (a `LocalBusiness` subtype — more precise than generic `LocalBusiness`):
  name, address, geo coordinates, phone, hours, price range, 24-city `areaServed`,
  `aggregateRating`, `review`, `hasOfferCatalog` with 5 services, `sameAs`.
- **`WebSite`** + **`WebPage`** nodes linked by `@id` (entity-first architecture).
- **`Service`** schema on each service page with `areaServed` and price ranges.
- **`FAQPage`** on home, replacement, storm, repair, inspection, commercial, financing.
- **`HowTo`** on the storm-damage page ("what to do after hail") — strong AI-answer-engine format.
- **`ItemList`** for services and the 34-city coverage list.
- **`BreadcrumbList`** on every inner page.
- **`Review`** schema on the reviews page.

All blocks validated as parseable JSON in the audit; zero console/validator errors.

### 3.3 On-page keyword strategy

Each service page owns **one primary intent** with supporting long-tail coverage — no cannibalisation:

- *roof replacement Dallas* → also covers cost, tear-off vs. roof-over, warranty, GAF Timberline HDZ
- *hail damage roof repair Dallas* → also covers claim deadlines, deductible law, Xactimate, adjuster
- *roof leak repair Dallas* → also covers pipe boots, flashing, valleys, emergency tarping, 24/7
- *free roof inspection Dallas* → also covers pre-closing reports, annual cadence, 21-point checklist

**Local SEO signals built in:** 34 city sections with genuine neighborhood-level detail
(Lakewood plank sheathing, Frisco builder-defect windows, Richardson tree canopy, Rockwall
lake wind exposure), NAP consistency in header/footer/schema, geo meta tags, service-area table
with response times, and `areaServed` in schema.

---

## 4. Content quality (E-E-A-T)

- **Experience:** 17-year history, named crew with roles, specific project ("2,480 sq ft Lakewood,
  GAF HDZ Charcoal, April 2026"), 92% first-pass claim approval stat.
- **Expertise:** accurate trade detail — Xactimate scopes, soft-metal testing, ice & water shield,
  step vs. counter flashing, intake/exhaust ventilation balance, TPO mil thickness.
- **Authoritativeness:** GAF Master Elite, BBB A+, RCAT licence number, $2M liability.
- **Trust:** transparent pricing table, an explicit "what insurance does NOT cover" table,
  a **4-star review included alongside the 5-star ones**, and a note that "waiving deductibles is
  insurance fraud in Texas." Honesty signals outperform hype for high-ticket local services.
- **AI/answer-engine readiness:** direct-answer FAQ blocks, HowTo steps, tables, and definitions
  formatted so LLMs can quote them (and crawlers are explicitly allowed in `robots.txt`).

---

## 5. Performance audit (Core Web Vitals)

| Metric | Mobile (throttled) | Desktop | Target | Status |
|---|---|---|---|---|
| LCP | **2.1 s** | 0.8 s | < 2.5 s | ✅ Good |
| CLS | **0.000** | 0.000 | < 0.1 | ✅ Perfect |
| TBT (INP proxy) | **30 ms** | 0 ms | < 200 ms | ✅ Good |
| FCP | 1.3 s | 0.3 s | < 1.8 s | ✅ Good |
| Speed Index | 1.3 s | 0.3 s | < 3.4 s | ✅ Good |
| Homepage weight | 212 KiB | 849 KiB | — | ✅ Light |

### Techniques used (no frameworks, no build server needed)
1. **CSS + JS inlined per page** → one HTTP request, zero render-blocking round-trips.
2. **System font stack** → no webfont download, no FOIT, no layout shift.
3. **LCP image preloaded** with `fetchpriority="high"` + `imagesrcset` (700w / 960w / 1400w).
4. **WebP with JPEG fallback** via `<picture>` + `srcset` + `sizes` (all images 50–70% smaller in WebP).
5. **Explicit `width`/`height` on all images** → measured CLS of exactly 0.
6. **`loading="lazy"` + `decoding="async"`** on all below-fold images.
7. **Vanilla JS, ~4 KB, deferred semantics** → 0–30 ms total blocking time.
8. **`content-visibility`-friendly structure**, no jQuery, no icon font, no carousel library
   (inline SVG icon system instead).
9. Animation respects `prefers-reduced-motion`; no layout thrash on scroll (passive listeners).

---

## 6. Accessibility audit (WCAG 2.1 AA)

**axe-core result: 0 violations on all 17 pages.** Issues found during the audit and fixed:

| # | Issue found | Severity | Fix applied |
|---|---|---|---|
| 1 | CTA orange `#F26B21` on white = 2.94:1 | Serious | Introduced `#C2410C` (5.2:1) for all button/text orange; kept bright orange for decorative accents on dark |
| 2 | `--ok` green `#1E9E6A` on white = 2.8:1 | Serious | Darkened to `#12754A` (6.5:1) |
| 3 | Amber text `#F5A623` = 1.9:1 | Serious | Split token: `--star` for glyphs, `--star-text #8A5800` for text |
| 4 | Alert-band gradient had stops at ~4.2:1 | Serious | Re-tuned gradient so white text passes at every stop |
| 5 | Grey `#6B7B8A` small text = 4.0:1 | Serious | Darkened to `#59687A` (5.2:1) |
| 6 | `aria-label` on a plain `<span>` (stars) | Serious | Added `role="img"` |
| 7 | Logo `aria-label` didn't contain visible text | Serious | Removed redundant label; visible text is the accessible name |
| 8 | Top bar content outside any landmark | Moderate | Converted to `<aside aria-label>` |
| 9 | Heading jump h1 → h3 on 404 | Moderate | Corrected to h2 |
| 10 | Honeypot input had no id/label | Moderate | Unique id + associated label |
| 11 | **Content invisible without JS** (reveal animation hid everything) | Critical (found by design review) | Reveal styles now scoped to `.js` — no-JS users and crawlers see all content |
| 12 | Page-hero eyebrow rendered pale text on cream pill (CSS specificity bug) | Critical (found in visual QA) | Explicit `.phero p.eyebrow` rule + dark-scope eyebrow tokens |

**Also verified:** keyboard-reachable skip link (first Tab), visible `:focus-visible` rings on every
interactive element, `aria-expanded` on the menu button, Escape closes the drawer, form errors are
announced with `role="alert"` and `aria-invalid`, one H1 per page, semantic landmark structure.

---

## 7. Functional QA (Playwright, 17 pages)

| Test | Result |
|---|---|
| Console errors / page errors | ✅ none on any page |
| Broken images | ✅ none (after lazy-load scroll) |
| Horizontal overflow @ 390px | ✅ fixed — tables now scroll in their own container, grid children got `min-width:0` |
| Horizontal overflow @ 1440px | ✅ none |
| Mobile drawer open/close | ✅ |
| Sticky mobile call/CTA bar | ✅ appears < 900px |
| Form validation (empty, bad phone, bad ZIP) | ✅ 3 errors raised, then 2, inline messages shown |
| Valid submit → thank-you redirect | ✅ with `?src=` attribution param |
| Before/after slider | ✅ clip-path updates |
| Desktop dropdown menu (hover) | ✅ |
| Keyboard skip link on first Tab | ✅ |
| Mobile top bar layout | ✅ refined after visual QA (wrapped phone number) |

---

## 8. Deliverables & file map

```
dallas-roofing/
├── index.html … 404.html        # 17 production-ready pages (CSS+JS inlined)
├── sitemap.xml                  # 15 indexable URLs
├── robots.txt                   # + AI crawler allows
├── site.webmanifest
├── assets/img/                  # WebP + JPEG at 700/960/1400w, logo, favicon
├── src/
│   ├── style.css                # design system (single source of truth)
│   ├── app.js                   # ~4KB vanilla JS
│   └── pages/*.html             # page content with JSON front-matter
├── build.py                     # build: injects head, schema, nav, footer, sitemap
└── tools/
    ├── audit.py                 # 40+ SEO/a11y/link checks
    ├── a11y_audit.py            # axe-core WCAG 2.1 AA across all pages
    ├── functional_test.py       # Playwright interaction tests
    └── a11y-report.json         # machine-readable results
```

**To rebuild after editing content:** `python3 build.py` (regenerates all pages + sitemap).
**To re-audit:** `python3 tools/audit.py && python3 tools/a11y_audit.py && python3 tools/functional_test.py`.

---

## 9. Launch checklist (business items, not code)

| # | Item | Owner | Notes |
|---|---|---|---|
| 1 | Replace demo NAP: phone `(214) 555-0198`, address `4132 Maple Ave`, email | Client | Update `BIZ` dict in `build.py` → rebuild |
| 2 | Replace RCAT licence `#RC-118402` with the real number | Client | Footer + schema |
| 3 | Replace all reviews with real, attributable ones | Client | Keep the 4-star one — it adds credibility |
| 4 | Wire forms to a real endpoint | Dev | In `src/app.js`, replace the demo `setTimeout` redirect with `fetch('/api/lead', …)`; keep the `generate_lead` / `fbq('Lead')` hooks |
| 5 | Add GA4 + Google Ads / Meta pixels | Dev | Hooks are pre-placed and commented in `app.js` |
| 6 | Verify `aggregateRating` against Google's review-snippet policy | SEO | Only publish ratings you can substantiate; otherwise remove that block |
| 7 | Create Google Business Profile + embed real map | Client | `hasMap` currently a placeholder |
| 8 | Publish 4–6 blog articles (outlines already on `blog.html`) | Content | Each article should target one long-tail query |
| 9 | Enable server compression + long cache headers for `/assets` | Host | Lighthouse flags ~80 KiB savings on uncompressed HTML |
| 10 | Submit sitemap in Google Search Console + Bing Webmaster | SEO | After DNS is live |
| 11 | Attorney review of privacy/terms (currently demo copy) | Client | Marked as sample text in the pages |
| 12 | Consider per-city landing pages | SEO | `service-areas.html` anchors are step one; 34 dedicated city pages are the scale play |

---

## 10. Honest limitations

- **The demo data is fictional** — company name, phone, licence, address, reviews and pricing are
  illustrative. They are clearly labelled as demo content in the footer.
- **Forms have no backend.** They validate fully and redirect to `thank-you.html`, but nothing is
  delivered until item 4 above is done.
- **Scores are from a local static server.** On shared hosting without compression, expect
  performance to drop a few points until item 9 is complete. The code itself is the same.
- **Schema `aggregateRating` and `Review` markup on your own site** can trigger Google's
  self-serving review policy. Item 6 covers this — it's a policy decision, not a bug.
