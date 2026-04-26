# Plainworks.ai Landing Page

Single-page static landing site for [Plainworks.ai](https://www.plainworks.ai).

## Repository Structure

```
plainworks-landing/
├── index.html              # Main landing page (32KB, self-contained)
├── audit/
│   └── index.html          # AI Audit self-assessment tool
├── blog/
│   ├── index.html          # Blog listing page
│   ├── posts/              # Blog post source files (Markdown)
│   │   ├── 01-the-solo-founders-ai-stack.md
│   │   ├── 02-why-most-smbs-fail-at-ai.md
│   │   ├── 03-from-40-hours-to-4.md
│   │   └── 04-the-ai-audit-framework.md
│   └── *.html              # Generated static blog pages
├── .github/workflows/
│   └── deploy.yml          # GitHub Actions auto-deploy pipeline
├── CNAME                    # Custom domain for GitHub Pages
├── netlify.toml             # Netlify security headers
├── robots.txt               # SEO: allow all crawlers
├── sitemap.xml              # SEO: sitemap for search engines
├── ANALYTICS-SETUP.md       # Google Analytics 4 configuration
├── SEO-FOUNDATION.md        # SEO documentation
└── README.md               # This file
```

## What's Included

### Landing Page (`index.html`)
- Self-contained landing page with embedded CSS and minimal JS (~32KB)
- **Hero** — Value proposition, dual CTAs, key stats
- **Services** — Three tier cards: AI Audit ($2,500), AI Enablement ($7,500), AI Native ($5,000/mo)
- **Trust** — Client logos + testimonial cards
- **Lead Magnet** — Newsletter signup for Free AI Audit Checklist
- **Contact** — Booking form with tier prefill

### AI Audit Self-Assessment (`audit/index.html`)
- Interactive 24-question assessment tool
- Scores 6 operational areas: Tools, Workflow, Marketing, Service, Data, Security
- Generates personalized action plan
- Print-friendly for offline use

### Blog
- 4 blog posts covering AI strategy and case studies
- Markdown source files in `blog/posts/`
- Static HTML pages generated from markdown

## Deployment

### GitHub Pages (Recommended — Free, Auto-SSL)

The site auto-deploys via GitHub Actions on every push to `main`.

1. **Enable GitHub Pages:**
   - Go to repo → Settings → Pages
   - Source: GitHub Actions

2. **Add custom domain:**
   - Settings → Pages → Custom domain: `www.plainworks.ai`
   - DNS must have CNAME record pointing to GitHub Pages

3. **DNS Configuration:**
   ```
   Type: CNAME
   Name: www
   Value: npw1980.github.io  (your GitHub Pages URL)
   ```

4. **Deploy:**
   - Push to `main` branch
   - GitHub Actions builds and deploys automatically
   - Takes ~2-3 minutes

### Netlify (Alternative)

1. Drag `plainworks-landing/` folder to [netlify.com](https://netlify.com) drop zone
2. Or connect via Git integration
3. Custom domain in Site Settings → Domain Management

### Cloudflare Pages / Vercel

See full deployment options in [DEPLOYMENT.md](./DEPLOYMENT.md) (if present).

## How to Update Content

### Update the Landing Page Text

Edit `index.html` directly. Key sections:
- **Hero headline:** Find `<h1>Stop drowning...` around line 300
- **Pricing tiers:** Find the `.tier-card` sections around line 350
- **Testimonials:** Find `.testimonial` blocks around line 400
- **Contact info:** Find `.contact-method` sections around line 440
- **Footer links:** Find `<footer>` around line 480

### Update Pricing

1. Open `index.html`
2. Find the pricing tier you want to update (search for `$2,500`, `$7,500`, etc.)
3. Update the price in three places per tier:
   - `.tier-price` div
   - `onclick="prefillTier('...')"` handler
   - `value="AI Audit"` option in the contact form select
4. Also update the JSON-LD structured data in `<head>` (schema.org prices)

### Add a New Blog Post

1. **Create the markdown file:**
   ```bash
   cp blog/posts/04-the-ai-audit-framework.md blog/posts/05-new-post-slug.md
   ```

2. **Edit the frontmatter:**
   ```yaml
   ---
   title: "Your New Post Title"
   slug: "your-new-post-slug"
   description: "Meta description for SEO"
   author: "Nathan White"
   author_role: "Founder, Plainworks.ai"
   published_date: "2026-06-01T08:00:00Z"
   category: "AI Strategy"
   tags: ["tag1", "tag2"]
   read_time: "8 min"
   canonical_url: "https://plainworks.ai/blog/your-new-post-slug.html"
   featured: false
   og_image: "https://plainworks.ai/assets/og-default.jpg"
   seo_title: "Your SEO Title | Plainworks"
   seo_description: "Your meta description for search results"
   primary_keyword: "primary keyword"
   status: "published"
   ---
   ```

3. **Generate the HTML page:**
   - Use any Markdown-to-HTML converter
   - Copy the structure from existing blog posts
   - Save as `blog/your-new-post-slug.html`

4. **Update blog listing:**
   - Edit `blog/index.html`
   - Add a new `<article class="blog-card">` block with the post info

5. **Update sitemap.xml:**
   - Add a new `<url>` entry for the new post

### Update the AI Audit Self-Assessment

Edit `audit/index.html`:
- **Questions:** Find `<div class="question">` blocks
- **Scoring logic:** JavaScript at the bottom handles scoring and recommendations
- **Recommendations:** Search for the `recs` object to customize recommendations

### Update Analytics Tracking

Google Analytics 4 is configured with ID `G-PLAINWORKS`:
- Change in `<head>` of all HTML files: `gtag('config', 'G-PLAINWORKS')`
- See `ANALYTICS-SETUP.md` for detailed tracking setup

## Known Issues and Workarounds

### Issue: Forms Show Demo Alerts
**Workaround:** Forms currently show `alert()` dialogs instead of sending data.

To make them functional, choose one:
1. **Formspree** (free tier: 50 submissions/month)
   - Register at formspree.io
   - Replace `onsubmit="handleSignup(event)"` with Formspree form action
2. **Getform** (free tier: 100 submissions/month)
   - Register at getform.io
   - Update form `action` attribute
3. **Netlify Forms** (if hosting on Netlify)
   - Add `netlify` attribute to form tags

### Issue: Forms Don't Pre-fill Service Tier
**Workaround:** The `prefillTier()` JavaScript function handles this:
```javascript
function prefillTier(tierName) {
  const select = document.getElementById('tier');
  if (select) {
    for (let i = 0; i < select.options.length; i++) {
      if (select.options[i].value === tierName) {
        select.selectedIndex = i;
        break;
      }
    }
  }
  document.getElementById('contact').scrollIntoView({ behavior: 'smooth' });
}
```

### Issue: Placeholder Testimonials and Logos
**Workaround:** When real testimonials and client logos are available:
1. Testimonials: Edit the `<blockquote>` content in `index.html`
2. Logos: Replace `<span>AgencyOwner</span>` with actual SVG/image logos

### Issue: Google-Site-Verification Placeholder
**Workaround:** The placeholder `<meta name="google-site-verification" content="google-site-verification-content" />` needs to be replaced with the actual verification code from Google Search Console.

### Issue: JSON-LD Schema Points to Missing Assets
**Workaround:** The structured data references `og-default.jpg`, `logo.png` assets. Either:
1. Add these images to an `/assets/` folder
2. Remove the references from the JSON-LD if images don't exist yet

### Issue: Blog Posts Are Static HTML
**Workaround:** For easier content management:
1. Consider switching to a static site generator (11ty, Hugo, Astro)
2. Or use Netlify CMS / Decap CMS for Git-based CMS
3. Current system works fine but requires manual HTML generation

## Technical Debt / Recommended Improvements

### High Priority

1. **Form Backend Integration**
   - Wire up Formspree, Getform, or similar for lead capture
   - Currently all form submissions are lost

2. **CMS for Blog Posts**
   - Moving to 11ty or Astro would allow Markdown authoring
   - Current system requires manual HTML generation

3. **Proper OG Images**
   - Create branded OG images for social sharing
   - Required for effective LinkedIn/Twitter promotion

### Medium Priority

4. **HTTPS Enforcement on Root Domain**
   - `plainworks.ai` (apex) should redirect to `www.plainworks.ai`
   - Add redirect rules to DNS provider or Cloudflare

5. **Contact Form Storage**
   - Consider integrating with a CRM or email service
   - Airtable + Zapier is a simple free option

6. **Analytics Enhancement**
   - Set up Google Search Console properly with real verification
   - Add conversion tracking for specific service tier CTAs

### Lower Priority

7. **Accessibility Audit**
   - Add ARIA labels where needed
   - Ensure keyboard navigation works throughout

8. **Performance Optimization**
   - Inline critical CSS (already done)
   - Lazy-load images below the fold
   - Add `preconnect` for Google Fonts

9. **Email Service for Newsletter**
   - Integrate ConvertKit, Mailchimp, or Buttondown
   - Currently newsletter signup goes nowhere

10. **Mobile App (Future)**
    - Consider a simple PWA for audit tool
    - Would allow offline access to assessment

## Cost Summary

| Component | Cost |
|-----------|------|
| Domain (plainworks.ai) | ~$12/year |
| Hosting (GitHub Pages) | Free |
| SSL | Free |
| Form Backend (Formspree) | Free tier |
| Analytics (GA4) | Free |
| **Total Monthly** | **~$1/year** |

## Quick Reference

| Task | File | Section |
|------|------|---------|
| Change hero text | `index.html` | `.hero` |
| Update prices | `index.html` | `.tier-card` |
| Add testimonial | `index.html` | `.testimonials` |
| Change email | `index.html` | `.contact-method` |
| Add blog post | `blog/posts/*.md` + `blog/*.html` | Blog listing |
| Edit audit questions | `audit/index.html` | `.question` |
| Update SEO meta | `index.html` | `<head>` meta tags |
| Change GA4 ID | All HTML files | `gtag('config', '...')` |

## Support

For technical issues with this site, contact the Plainworks technical team or refer to the [AGENTS.md](./AGENTS.md) file for development context.
