# Analytics & Conversion Tracking Setup — Plainworks.ai

## 1. Google Analytics 4 — Setup Instructions

### Create the Property
1. Go to [Google Analytics](https://analytics.google.com) and sign in with the Google account that owns `plainworks.ai`.
2. Click **Admin** (gear icon) → **Create** → **Property**.
3. Property name: `Plainworks.ai`
4. Time zone: `United States`
5. Currency: `USD`
6. Industry: `Professional Services`
7. Business size: `Small`
8. Click **Next**, select your business objectives (recommend: `Generate leads`, `Raise brand awareness`), then **Create**.
9. Choose **Web** as the data stream.
10. Website URL: `https://plainworks.ai`
11. Stream name: `Plainworks.ai Web`
12. Enable **Enhanced measurement** (page views, scrolls, outbound clicks, site search, form interactions, video engagement, file downloads).
13. Click **Create stream**.
14. Copy the **Measurement ID** (looks like `G-XXXXXXXXXX`).

### Replace the Placeholder ID
The tracking code is already embedded in every HTML file. Search and replace `G-PLAINWORKS` with your real Measurement ID across the repo:

```bash
grep -rl 'G-PLAINWORKS' . | xargs sed -i 's/G-PLAINWORKS/G-XXXXXXXXXX/g'
```

(Replace `G-XXXXXXXXXX` with your actual ID.)

### Files with GA4 installed
- `index.html` — Landing page
- `blog/index.html` — Blog index
- `blog/the-solo-founders-ai-stack.html`
- `blog/why-most-smbs-fail-at-ai.html`
- `blog/from-40-hours-to-4.html`
- `blog/the-ai-audit-framework.html`
- `audit/index.html` — AI Audit self-assessment

---

## 2. Google Search Console — Setup Instructions

### Verify Site Ownership
**Method recommended:** HTML meta tag (already embedded).

1. Go to [Google Search Console](https://search.google.com/search-console).
2. Click **Add property** → **Domain** or **URL prefix**.
3. If using **URL prefix**, enter `https://plainworks.ai/`.
4. Choose **HTML tag** verification method.
5. Copy the `content` value from the meta tag (looks like a long string of letters and numbers).
6. Replace `google-site-verification-content` in every HTML file with this real value:

```bash
grep -rl 'google-site-verification-content' . | xargs sed -i 's/google-site-verification-content/YOUR_REAL_CONTENT/g'
```

7. Click **Verify** in Search Console.

### Submit the Sitemap
1. In Search Console, select your property.
2. Go to **Sitemaps** in the left sidebar.
3. Enter `sitemap.xml` in the **Add a new sitemap** field.
4. Click **Submit**.

---

## 3. Conversion Event Tracking

Custom events are implemented via `data-track` attributes and a lightweight event-delegation script. No external libraries required.

### Events Tracked

| Event Name | Trigger | Parameters | Pages |
|-----------|---------|-----------|-------|
| `page_view` | Automatic (GA4) | — | All pages |
| `blog_post_view` | Page load on blog posts | `post_title`, `page_path` | Blog posts |
| `cta_click` | Click on any tracked button/link | `cta_name`, `cta_location` | Landing, blog index, blog posts |
| `newsletter_signup` | Submit lead-magnet email form | `form_id`, `form_type`, `form_location` | Landing page |
| `contact_form_submit` | Submit contact form | `form_id`, `form_type`, `form_location` | Landing page |
| `blog_post_click` | Click blog post card link | `post_title` | Blog index |
| `audit_start` | Page load on audit page | `page_path` | Audit page |
| `audit_progress` | First answer selected | `page_path`, `milestone: first_answer` | Audit page |
| `audit_completion` | Submit with all 24 questions answered | `page_path`, `questions_answered` | Audit page |
| `audit_book_click` | Click "Book a Full AI Audit" in results | `cta_location` | Audit page |

### Adding New Events
To track any new element, add `data-track="event_name"` and optional `data-*` parameters:

```html
<a href="/pricing" data-track="cta_click" data-cta-name="pricing_nav" data-cta-location="header">Pricing</a>
```

---

## 4. Weekly Metrics Dashboard

Review these **5–7 key metrics** every Monday morning in GA4. Each includes where to find it and what action to take.

### 1. Total Users
- **Where:** GA4 → Reports → Engagement → Overview → Users
- **What it tells you:** Raw reach. Are people finding the site?
- **Target:** 100+ users/week by Month 2.
- **Action if low:** Increase LinkedIn/X posting frequency; check that sitemap is indexed.

### 2. Sessions by Traffic Source
- **Where:** GA4 → Reports → Acquisition → Traffic acquisition
- **What it tells you:** Which channels are working (organic search, direct, social, referral).
- **Target:** Organic search = 30%+, Direct = 25%+, Social = 20%+.
- **Action if skewed:** If social > 50%, SEO is underperforming — publish more blog posts and build backlinks.

### 3. Average Engagement Time
- **Where:** GA4 → Reports → Engagement → Overview → Average engagement time
- **What it tells you:** Are visitors actually reading or bouncing immediately?
- **Target:** > 45 seconds on landing page; > 2 minutes on blog posts.
- **Action if low:** Tighten hero copy; add more subheadings and visuals to blog posts.

### 4. Blog Post Views (by post)
- **Where:** GA4 → Reports → Engagement → Pages and screens → Filter by `/blog/`
- **What it tells you:** Which topics resonate most with your audience.
- **Action:** Double down on the top-performing topic; refresh or expand the lowest-performing post.

### 5. CTA Click Rate
- **Where:** GA4 → Configure → Events → Search for `cta_click` → Click the event → Add comparison by `cta_name`
- **What it tells you:** Which calls-to-action drive action.
- **Target:** > 3% of sessions click a primary CTA (`see_pricing`, `start_build`, `book_audit`).
- **Action if low:** A/B test button copy or color; move CTA higher on the page.

### 6. Self-Assessment Completion Rate
- **Where:** GA4 → Configure → Events → Compare `audit_start` vs `audit_completion`
- **What it tells you:** How compelling and usable the self-assessment is.
- **Target:** > 25% of starters complete all 24 questions.
- **Action if low:** Reduce questions; add progress reminders; test a shorter 10-question version.

### 7. Contact Form / Newsletter Conversion Rate
- **Where:** GA4 → Configure → Events → Compare `contact_form_submit` + `newsletter_signup` against total users
- **What it tells you:** How well the site converts visitors into leads.
- **Target:** > 2% combined conversion rate.
- **Action if low:** Strengthen social proof above the form; reduce form fields; test a popup on blog posts.

### Optional: Search Console Integration
- **Where:** Link GA4 to Search Console (Admin → Product links → Search Console links).
- **Metrics to watch:** Average position, click-through rate (CTR), top queries.
- **Action:** If a blog post ranks #5–10 for a high-intent keyword, add an internal link to it from the landing page to boost authority.

---

## 5. Privacy Compliance Note

### Do You Need a Cookie Consent Banner?

**Short answer: Yes, for full compliance.**

Google Analytics 4 uses first-party cookies (`_ga`, `_ga_*`) to persist user IDs and session data. Under:
- **GDPR** (EU/UK visitors): You need explicit consent before loading GA4.
- **CCPA/CPRA** (California visitors): You need a "Do Not Sell/Share" opt-out mechanism.
- **Other US states** (Virginia, Colorado, Connecticut, Utah): Similar opt-out requirements apply.

Even if your primary audience is US-based today, you will likely attract EU/UK visitors through LinkedIn, X, and search.

### Recommended Lightweight Solution: Cookiebot or Osano (Free Tier)

**Option A: Cookiebot by Usercentrics (Free up to 1 pageview/month)**
- Sign up at [cookiebot.com](https://www.cookiebot.com)
- Add the consent banner script to the `<head>` of every page **before** the GA4 script.
- Configure to block GA4 until consent is given.
- Cost: Free under the limit; paid plans start at ~$15/month.

**Option B: Osano (Free tier)**
- Sign up at [osano.com](https://www.osano.com)
- Simple script insertion; auto-detects cookies.
- Cost: Free for basic compliance; paid plans for advanced features.

**Option C: DIY Minimal Consent Banner (No cost)**
If budget is zero, add a simple banner that:
1. Appears on first visit.
2. Explains GA4 is used for anonymous analytics.
3. Has an "Accept" and "Decline" button.
4. Only loads the GA4 script if the user clicks "Accept."

Example minimal banner code (can be added to a shared script):

```html
<div id="cookie-banner" style="position:fixed;bottom:0;left:0;right:0;background:#1f2937;color:#f3f4f6;padding:16px 24px;font-size:14px;z-index:999;display:none;">
  <div style="max-width:1120px;margin:0 auto;display:flex;flex-wrap:wrap;gap:12px;align-items:center;justify-content:space-between;">
    <span>We use cookies to understand how visitors use our site. No personal data is sold.</span>
    <div style="display:flex;gap:10px;">
      <button onclick="acceptCookies()" style="padding:8px 16px;background:#22d3ee;color:#0b0f19;border:none;border-radius:8px;font-weight:600;cursor:pointer;">Accept</button>
      <button onclick="declineCookies()" style="padding:8px 16px;background:transparent;color:#f3f4f6;border:1px solid #374151;border-radius:8px;cursor:pointer;">Decline</button>
    </div>
  </div>
</div>
<script>
  function acceptCookies() { localStorage.setItem('cookie_consent', 'accepted'); document.getElementById('cookie-banner').style.display='none'; loadGA4(); }
  function declineCookies() { localStorage.setItem('cookie_consent', 'declined'); document.getElementById('cookie-banner').style.display='none'; }
  if (localStorage.getItem('cookie_consent') === null) document.getElementById('cookie-banner').style.display='block';
  if (localStorage.getItem('cookie_consent') === 'accepted') loadGA4();
</script>
```

### Immediate Action Items for Nathan
1. [ ] Replace `G-PLAINWORKS` with real GA4 Measurement ID.
2. [ ] Replace `google-site-verification-content` with real GSC verification string.
3. [ ] Verify site in Google Search Console and submit `sitemap.xml`.
4. [ ] Choose and implement a cookie consent solution before driving significant paid traffic.
5. [ ] Set up a weekly calendar reminder to review the 7 metrics above.

---

## 6. Analytics Access for Nathan White

### Google Analytics 4
**Account:** To be created at [analytics.google.com](https://analytics.google.com)

**Access Instructions:**
1. Create a Google Analytics 4 property using the email associated with `plainworks.ai`
2. Once created, share access with `nathanpwhite@gmail.com` with "Editor" permissions
3. Measurement ID format: `G-XXXXXXXXXX` (replace in all HTML files once obtained)

### Google Search Console
**Account:** To be verified at [search.google.com/search-console](https://search.google.com/search-console)

**Access Instructions:**
1. Verify ownership using the HTML meta tag (already embedded)
2. Once verified, add `nathanpwhite@gmail.com` as an owner or user

### Analytics Documentation Location
All analytics documentation is stored in the `npw1980/plainworks-landing` repo:
- `ANALYTICS-SETUP.md` — Complete setup guide and weekly metrics dashboard
- `UTM-GUIDELINES.md` — UTM parameter naming conventions and campaign tracking
- `SEO-FOUNDATION.md` — Technical SEO documentation

---

## 7. Files Modified for PLA-56

| File | Change |
|------|--------|
| `index.html` | GA4 tracking code (placeholder ID `G-PLAINWORKS`)
| `blog/index.html` | GA4 tracking + conversion events
| `blog/*.html` | GA4 tracking + blog post view events
| `audit/index.html` | GA4 tracking + audit funnel events
| `UTM-GUIDELINES.md` | **NEW** — UTM parameter standards
| `ANALYTICS-SETUP.md` | Updated with access section and file manifest

---

*Last updated: 2026-04-26 (PLA-56)*
