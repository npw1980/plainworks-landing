# Plainworks.ai Landing Page

Single-page static landing site for [Plainworks.ai](https://www.plainworks.ai).

## What's Included

- `index.html` — Self-contained landing page (~26KB) with embedded CSS and minimal JS
- `CNAME` — Custom domain configuration for GitHub Pages
- `netlify.toml` — Security headers for Netlify deployments
- `.github/workflows/deploy.yml` — Auto-deploy to GitHub Pages on every push to `main`

## Sections

1. **Hero** — Value proposition, dual CTAs, key stats
2. **Services** — Three tier cards (AI Audit $2,500, AI Enablement $7,500, AI Native $5,000/mo)
3. **Trust** — Placeholder client logos + testimonial cards
4. **Lead Magnet** — Newsletter signup for Free AI Audit Checklist
5. **Contact** — Booking form with tier prefill

## Deployment Options

### Option A: GitHub Pages (Recommended — Free, Custom Domain, Auto-SSL)

1. **Create a public GitHub repo** (e.g. `nathanwhite/plainworks-landing`)
2. **Push this code** to the `main` branch
3. **Enable Pages**:
   - Go to repo → Settings → Pages
   - Source: GitHub Actions
4. **Add custom domain**:
   - In Pages settings, enter `www.plainworks.ai`
   - GitHub will verify and provision an SSL certificate automatically
5. **DNS configuration** (see below)

The included GitHub Actions workflow will auto-deploy on every push.

### Option B: Netlify (Free Tier, Drag-and-Drop)

1. Go to [netlify.com](https://netlify.com) and sign up/log in
2. Drag the `plainworks-landing` folder onto the Netlify dashboard
3. Site deploys instantly to a `*.netlify.app` URL
4. Add custom domain:
   - Site settings → Domain management → Add custom domain
   - Enter `www.plainworks.ai`
   - Follow Netlify's DNS instructions

### Option C: Cloudflare Pages (Free, Great Performance)

1. Go to [cloudflare.com](https://cloudflare.com) → Pages
2. Create a project → Connect to Git or Direct Upload
3. Upload the folder contents
4. Add custom domain in project settings

### Option D: Vercel (Free Tier)

1. Go to [vercel.com](https://vercel.com) and import this repo
2. Framework preset: **Other** (static HTML)
3. Add custom domain in project settings

## DNS Configuration

### Using `www.plainworks.ai` (Recommended)

Create a **CNAME record** at your DNS provider:

| Type | Name | Value |
|------|------|-------|
| CNAME | www | nathanwhite.github.io |

*(Replace `nathanwhite.github.io` with your actual GitHub Pages URL, or your Netlify/Cloudflare/Vercel target.)*

### Using Apex Domain `plainworks.ai`

If you want the root domain to work, add these **A records** pointing to GitHub Pages IPs:

| Type | Name | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

Then add a **CNAME** for `www` → `plainworks.ai` to ensure both work.

**Note:** Some DNS providers (Cloudflare, Namecheap, GoDaddy) support CNAME flattening at the apex, which lets you use a CNAME for `@`. Check with your provider.

## SSL / HTTPS

All recommended hosts (GitHub Pages, Netlify, Cloudflare Pages, Vercel) provision and renew SSL certificates automatically at no cost. No manual cert management needed.

## Cost Estimate

| Service | Hosting | Custom Domain | SSL | Monthly Cost |
|---------|---------|---------------|-----|-------------|
| GitHub Pages | Free | Free | Free | **$0** |
| Netlify | Free tier | Free | Free | **$0** |
| Cloudflare Pages | Free | Free | Free | **$0** |
| Vercel | Free tier | Free | Free | **$0** |

Domain registration for `plainworks.ai` is separate (~$10-15/year at Namecheap, Cloudflare Registrar, etc.)

## Next Steps After Deploy

1. **Connect form backends** — The signup and contact forms currently show demo alerts. Wire up:
   - [Formspree](https://formspree.io) (free tier: 50 submissions/mo)
   - [Getform](https://getform.io) (free tier: 100 submissions/mo)
   - Or a serverless function (Vercel/Netlify Functions, Cloudflare Workers)

2. **Swap placeholders** — Replace placeholder testimonials and client logos with real content when available

3. **Analytics** — Add Plausible, Fathom, or Google Analytics to track conversions

4. **SEO** — Submit sitemap to Google Search Console once live
