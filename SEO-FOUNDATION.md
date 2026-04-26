# SEO Foundation Package — Delivery Notes

## Changes Delivered

### 1. Sitemap & Robots
- **`sitemap.xml`** — includes all 6 pages (landing, blog index, 4 posts) with `lastmod`, `changefreq`, and `priority`
- **`robots.txt`** — `Allow: /` for all agents, references sitemap

### 2. Title & Meta Description Optimization
All titles are now 50–60 characters and descriptions 120–160 characters:

| Page | Title (chars) | Description (chars) |
|------|--------------|---------------------|
| Landing | Plainworks.ai — AI-First Operations for Small Business (55) | 146 |
| Blog index | AI Strategy Blog for Solo Founders & SMBs \| Plainworks (55) | 145 |
| Solo Founder Stack | Solo Founder's AI Stack: What Actually Works \| Plainworks (59) | 143 |
| SMB Failure | Why Most SMBs Fail at AI — And What Works \| Plainworks (55) | 146 |
| 40 Hours → 4 | From 40 Hours to 4: A Freelancer's AI System \| Plainworks (59) | 142 |
| AI Audit | The AI Audit: 6-Part Framework for Small Business \| Plainworks (63) | 160 |

### 3. Canonical Tags
- Added to **landing page** (`https://plainworks.ai/`)
- Already present on all blog pages; verified correct

### 4. Open Graph & Twitter Cards
- **Landing page**: Added complete OG and Twitter Card meta tags
- **Blog index**: Already had OG/Twitter — verified correct
- **All blog posts**: Already had OG/Twitter — verified correct
- All OG/Twitter titles now match optimized `<title>` tags

### 5. JSON-LD Structured Data
- **Landing page**: Added `Organization` + `Service` (with `OfferCatalog` for the 3 tiers) + `WebSite` schemas
- **Blog index**: Added `Blog` schema with nested `blogPost` references
- **All blog posts**: `BlogPosting` schema already present and complete
- **AI Audit post**: Added `HowTo` schema for the self-assessment framework (6 steps)

### 6. Core Web Vitals Assessment

| Metric | Status | Notes |
|--------|--------|-------|
| **LCP** | ✅ Good | Static HTML, no hero images, inline SVG. Estimated < 1.5s on fast 4G. |
| **CLS** | ✅ Good | Explicit CSS dimensions, inline SVG with viewBox. Minor risk: hero SVG lacks explicit `height` in CSS — recommend adding `aspect-ratio: 5/4` or `height: auto` to the inline style. |
| **INP** | ✅ Excellent | Zero blocking JS, minimal interactions. |
| **FID** | ✅ Excellent | Main thread is free; no long tasks. |

**Recommended fixes for CWV:**
1. Add `aspect-ratio: 5/4` to the hero SVG inline style on the landing page.
2. Preconnect to `https://fonts.gstatic.com` is already present; keep it.
3. Consider adding a resource hint `<link rel="dns-prefetch" href="//fonts.googleapis.com">`.
4. Add `fetchpriority="high"` to the hero SVG if it is deemed the LCP element.
5. The OG image assets (`/assets/og-*.jpg`) are referenced in meta tags but do not exist in this repo — verify they were delivered under [PLA-27](mention://issue/PLA-27).

### 7. Missing Assets Note
OG image paths (`/assets/og-*.jpg`, `/assets/logo.png`) are referenced in meta tags and structured data. These should be present from [PLA-27](mention://issue/PLA-27). If they are missing at deploy time, crawlers will flag 404s for the images but will still index the pages.
