# Plainworks.ai Operations Runbook

**For:** Nathan White  
**Purpose:** Update the Plainworks.ai website without needing technical help  
**Last Updated:** April 2026

---

## Overview

The Plainworks.ai website is a static HTML site hosted on GitHub Pages. It auto-deploys when changes are pushed to the `main` branch. The site consists of:

- **Landing page** — Main sales page with services, testimonials, contact form
- **Blog** — Articles about AI strategy and case studies
- **AI Audit tool** — Interactive self-assessment questionnaire

All files are plain HTML/CSS — no database, no CMS. You edit text, commit, and it goes live automatically.

---

## Quick Reference Card

| What you want to do | Where to edit | Estimated time |
|---------------------|---------------|----------------|
| Update hero headline | `index.html` → `.hero` section | 5 minutes |
| Change a price | `index.html` → three places per tier | 5 minutes |
| Update a testimonial | `index.html` → `.testimonials` section | 5 minutes |
| Add a new blog post | New markdown file + `blog/index.html` | 30 minutes |
| Fix a typo anywhere | Edit the relevant `.html` file | 2 minutes |
| Update contact info | `index.html` → `.contact-method` section | 5 minutes |

---

## How the Site Works (Plain English)

Think of the website like a Google Doc that automatically publishes itself.

1. **You edit files** in the GitHub repository
2. **GitHub automatically builds** the site when you push changes
3. **The site goes live** within 2-3 minutes

No manual upload, no FTP, no hosting panel. Just edit → push → live.

---

## Task 1: Update the Landing Page Text

### Step 1: Go to the GitHub Repository

1. Open [github.com/npw1980/plainworks-landing](https://github.com/npw1980/plainworks-landing)
2. Click on `index.html`
3. Click the pencil icon (Edit) in the top right

### Step 2: Find the Text You Want to Change

Use Ctrl+F (or Cmd+F on Mac) to search for keywords. Common searches:

| What you want to change | Search for |
|------------------------|------------|
| Main headline | `Stop drowning in busywork` |
| Subheadline | `Plainworks.ai helps sole proprietors` |
| AI Audit description | `A full diagnostic` |
| Pricing | `$2,500` or `$7,500` or `$5,000` |
| Email address | `hello@plainworks.ai` |
| Availability | `Booking 2–3 weeks` |
| Testimonials | `In three weeks` or `I was skeptical` |

### Step 3: Make Your Edit

1. Make your changes in the text editor
2. Scroll to the bottom
3. Write a short commit message like "Updated hero headline" or "Fixed pricing"
4. Click **Commit changes**

The site will update automatically within 2-3 minutes.

---

## Task 2: Change Pricing

### Important: Prices appear in THREE places per tier

For each price change, you must update all three locations:

**Example: Changing AI Audit from $2,500 to $2,000**

1. Find `$2,500` — change the display price
2. Find `value="AI Audit"` — change the option value
3. Find `onclick="prefillTier('AI Audit')"` — this one stays the same (it's the button label)

### The Three Tiers

| Tier | Display Price | Select Option | Button Function |
|------|--------------|---------------|-----------------|
| AI Audit | `$2,500` | `value="AI Audit"` | `prefillTier('AI Audit')` |
| AI Enablement | `$7,500` | `value="AI Enablement"` | `prefillTier('AI Enablement')` |
| AI Native | `$5,000<span>/month</span>` | `value="AI Native"` | `prefillTier('AI Native')` |

---

## Task 3: Update Testimonials

### Step 1: Navigate to the Testimonials Section

1. Go to [index.html](https://github.com/npw1980/plainworks-landing/blob/main/index.html)
2. Press Ctrl+F and search for `testimonial`

### Step 2: Edit the Testimonial Block

Each testimonial looks like this:

```html
<div class="testimonial">
  <blockquote>"Your testimonial text goes here."</blockquote>
  <cite>
    <div class="avatar">AB</div>
    <div>
      <strong>Name Here</strong>
      <span>Job Title, City</span>
    </div>
  </cite>
</div>
```

### Step 3: Make Your Changes

1. Replace the quote text inside `""`
2. Replace `Name Here` with the person's name
3. Replace `AB` with their initials (first and last name)
4. Replace `Job Title, City` with their title and location
5. Click **Commit changes**

---

## Task 4: Add a New Blog Post

### Step 1: Create the Markdown File

1. Go to the repo → `blog/posts/` folder
2. Click **Add file** → **Create new file**
3. Name it: `05-your-post-slug.md`

### Step 2: Copy This Template

```markdown
---
title: "Your Post Title Here"
slug: "your-post-slug"
description: "A brief description for search engines and social media."
author: "Nathan White"
author_role: "Founder, Plainworks.ai"
published_date: "2026-06-01T08:00:00Z"
modified_date: "2026-06-01T08:00:00Z"
category: "AI Strategy"
tags: ["tag1", "tag2"]
read_time: "8 min"
canonical_url: "https://plainworks.ai/blog/your-post-slug.html"
featured: false
og_image: "https://plainworks.ai/assets/og-default.jpg"
seo_title: "Your SEO Title | Plainworks"
seo_description: "Your meta description."
primary_keyword: "primary keyword"
status: "published"
---

Your blog post content goes here. Write in plain English. Use markdown formatting:

## This is a heading
Normal paragraph text.

### This is a subheading
- Bullet point 1
- Bullet point 2

**Bold text** and *italic text* work too.

---

*End with a call-to-action that links to your services.*
```

### Step 3: Commit the File

1. Write a commit message: "Add new blog post: Your Post Title"
2. Click **Commit new file**

### Step 4: Update the Blog Listing Page

1. Open `blog/index.html`
2. Find an existing `<article class="blog-card">` block
3. Copy it and update:
   - `date`: Month Year
   - `h2`: Your post title
   - `href`: Link to your post slug
   - `p class="excerpt"`: Your excerpt
4. Move it to the top (most recent first)
5. Commit the changes

### Step 5: Update the Sitemap

1. Open `sitemap.xml`
2. Add a new `<url>` entry:
```xml
<url>
  <loc>https://plainworks.ai/blog/your-post-slug.html</loc>
  <lastmod>2026-06-01</lastmod>
  <changefreq>monthly</changefreq>
  <priority>0.8</priority>
</url>
```

---

## Task 5: Update Contact Information

### Step 1: Find the Contact Section

1. Open `index.html`
2. Search for `contact-method`

### Step 2: Update Email

Find and change:
```html
<strong>Email</strong>
<span>hello@plainworks.ai</span>
```

### Step 3: Update Availability

Find and change:
```html
<strong>Availability</strong>
<span>Booking 2–3 weeks out</span>
```

---

## Task 6: Fix the Google Verification Code

Currently, the Google Search Console verification is a placeholder. To fix it:

1. Go to [Google Search Console](https://searchconsole.google.com)
2. Add your property (plainworks.ai)
3. Choose **HTML tag** verification method
4. Copy the `<meta name="google-site-verification" content="...">` code
5. Open `index.html`
6. Search for `google-site-verification`
7. Replace the placeholder content with your actual verification code
8. Commit the change

---

## What NOT to Change Without Help

| Item | Why | Who to Ask |
|------|-----|------------|
| GitHub Actions workflow | Could break deployments | Plainworks Tech |
| CSS styles | May break the design | Plainworks Tech |
| JavaScript logic | May break forms/tracking | Plainworks Tech |
| JSON-LD structured data | SEO impact | Plainworks Tech |
| GitHub Pages settings | Could take site offline | Plainworks Tech |

---

## Troubleshooting

### The Site Isn't Updating

1. Wait 3-5 minutes (GitHub takes time to build)
2. Check the Actions tab on GitHub for errors
3. If there's a red X, contact Plainworks Tech with the error message

### I Made a Mistake

1. Go to the file on GitHub
2. Click **History**
3. Find the last good version
4. Click **Browse files** to view that version
5. Click the pencil → **Edit this file**
6. Commit the old version back

### I Accidentally Deleted Something

1. Go to **History** for that file
2. Find the commit that deleted it
3. Click **View** to see the old content
4. Copy the content back and commit

---

## Emergency: Take the Site Offline

If you need to take the site down urgently:

1. Go to repository **Settings**
2. Go to **Pages** in the left sidebar
3. Under **Source**, change from "GitHub Actions" to "None"
4. This stops the auto-deployment

To bring it back:
1. Change the source back to "GitHub Actions"
2. The next push to `main` will redeploy

---

## Get Help

For anything not covered here, contact the Plainworks technical team or create an issue in the repository with a description of what you need.

---

## Version History

| Date | Change | Who |
|------|--------|-----|
| April 2026 | Initial runbook | Plainworks CTO |
