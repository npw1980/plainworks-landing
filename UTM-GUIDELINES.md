# UTM Parameter Guidelines — Plainworks.ai

## Overview

UTM (Urchin Tracking Module) parameters are tags added to URLs to track the source, medium, and campaign of incoming traffic in Google Analytics. Consistent UTM naming ensures clean, actionable data.

## The 5 UTM Parameters

| Parameter | Required | Purpose | Example |
|-----------|----------|---------|---------|
| `utm_source` | ✅ Yes | Where the traffic comes from | `linkedin`, `twitter`, `google`, `newsletter` |
| `utm_medium` | ✅ Yes | The marketing medium | `social`, `cpc`, `email`, `referral`, `organic` |
| `utm_campaign` | Recommended | The specific campaign or promotion | `month2-launch`, `case-study-promo`, `lead-magnet` |
| `utm_term` | Optional | Paid search keyword (use sparingly) | `ai+consulting+small+business` |
| `utm_content` | Optional | Differentiate similar content or CTAs | `hero-button`, `sidebar-cta`, `email-header` |

## Naming Conventions

### Rules
1. **Always use lowercase** — GA4 is case-sensitive
2. **Use hyphens to separate words** — `utm_source=linkedin` not `utm_source=LinkedIn`
3. **Use underscores only for compound terms** — `utm_source=email_newsletter`
4. **Be consistent** — Create your source/medium list once and stick to it

### Source Values (utm_source)
```
linkedin       — LinkedIn posts or company page
twitter         — Twitter/X posts
facebook        — Facebook posts or page
instagram       — Instagram posts or profile
google          — Google Ads or organic search (prefer organic for non-ads)
newsletter      — Email newsletter issues
podcast         — Podcast show notes or descriptions
guest_post      — Guest blog post on another site
partner         — Partner or affiliate referral
direct          — Do NOT use; GA4 auto-detects direct traffic
```

### Medium Values (utm_medium)
```
social          — Any social media platform
cpc             — Paid search/display ads
email           — Email marketing
referral        — Non-partner website links
organic          — Organic (non-paid) search
affiliate       — Partner/affiliate links
video           — YouTube or video platform links
```

## Campaign Naming Guide

### Content Distribution
| Campaign Name | When to Use |
|--------------|-------------|
| `blog-launch` | Promoting a new blog post |
| `content-promotion` | General blog/social content push |
| `case-study-release` | New case study published |

### Lead Magnet Campaigns
| Campaign Name | When to Use |
|--------------|-------------|
| `lead-magnet-linkedin` | LinkedIn post driving to lead magnet |
| `newsletter-promo` | Email promoting lead magnet download |
| `blog-cta-push` | Blog posts linking to lead magnet |

### Event/Promotional Campaigns
| Campaign Name | When to Use |
|--------------|-------------|
| `launch-week` | New service or product launch |
| `webinar-promo` | Webinars or virtual events |
| `seasonal-offer` | Holiday or seasonal promotions |

## Example UTM URLs

### LinkedIn Post → Landing Page
```
https://plainworks.ai/?utm_source=linkedin&utm_medium=social&utm_campaign=month2-launch&utm_content=hero-cta
```

### Newsletter Issue → Blog Post
```
https://plainworks.ai/blog/the-solo-founders-ai-stack?utm_source=newsletter&utm_medium=email&utm_campaign=week6-issue&utm_content=blog-link
```

### Guest Post → Lead Magnet
```
https://plainworks.ai/#lead-magnet?utm_source=guest_post&utm_medium=referral&utm_campaign=smb-outreach&utm_content=inline-cta
```

### Twitter/X Post → Landing Page
```
https://plainworks.ai/?utm_source=twitter&utm_medium=social&utm_campaign=thought-leadership&utm_content=bio-link
```

## URL Builder Tools

### Google Campaign URL Builder
https://ga4-config.streamlit.app/ (or search "Campaign URL Builder" in Google)

### Quick Reference
```
Base URL: https://plainworks.ai

Required format:
https://plainworks.ai/[destination]?utm_source=[source]&utm_medium=[medium]&utm_campaign=[campaign]

Full format:
https://plainworks.ai/[destination]?utm_source=[source]&utm_medium=[medium]&utm_campaign=[campaign]&utm_term=[term]&utm_content=[content]
```

## Quick Checklist Before Sharing Any Link

- [ ] Using lowercase for all values
- [ ] Using hyphens between words
- [ ] `utm_source` and `utm_medium` are always included
- [ ] `utm_campaign` is descriptive (not "test" or "campaign1")
- [ ] Link is tested and redirects correctly
- [ ] Destination page matches the campaign intent

## How to View UTM Data in GA4

1. Go to **Reports** → **Acquisition** → **Traffic acquisition**
2. Set a comparison or filter for your campaign source/medium
3. Look at the **Session source/medium** and **Session campaign** dimensions
4. Cross-reference with engagement metrics (time on site, pages/session)

## Campaign Tracking Calendar

| Month | Campaign | Source | Medium | Notes |
|-------|----------|--------|--------|-------|
| Month 1 | Initial launch | linkedin | social | Brand awareness push |
| Month 1 | Blog promotion | newsletter | email | First 4 blog posts |
| Month 2 | Case studies | linkedin | social | New case study release |
| Month 2 | Partnership outreach | partner | referral | B2B partnership links |

---

*Document created: 2026-04-26*
