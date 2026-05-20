# Atlas Lead Pipeline — AI Prospecting Engine

> End-to-end AI lead intelligence system. Scrape → qualify → score → CRM → alert. Built for local service business prospecting at scale.

---

## What It Is

Atlas is CartierCreative's automated prospecting engine. It sources, qualifies, and imports leads from Google Maps into the CRM without manual input — then notifies the team in Slack with only the highest-quality targets.

**Real results:**
- 117 leads sourced
- 31 cold calls made
- 3 demos booked
- **9.7% call-to-demo rate**
- $0 in ad spend

---

## How It Works

```
Step 1 — SCRAPE (Atlas)
  Apify Google Maps Extractor
  Input: industry + city + filters (no website, min reviews)
  Output: raw business data JSON (name, phone, rating, review count, address)
        ↓

Step 2 — QUALIFY (Prometheus)
  Claude AI scores each lead 1–5:
    5 = No website, high reviews, plumber/roofer → P1 HOT
    3 = No website, low reviews → P2 WARM
    1 = Has website or wrong ICP → skip
        ↓

Step 3 — IMPORT
  Qualified leads appended to Google Sheets CRM
  Fields: Business Name, Phone, Industry, City, Lead Source,
          Website Status, Google Rating, Lead Quality Score,
          Status, Follow Up Date
        ↓

Step 4 — ALERT (Jarvis)
  Top picks (score 4–5) posted to Slack #leads channel
  Format: business name, phone, score, quick summary
```

---

## Lead Scoring Criteria

| Score | Criteria |
|---|---|
| **5** | No website · 10+ reviews · 4.5+ stars · target niche |
| **4** | No website · 5–10 reviews · 4.0+ stars |
| **3** | No website · under 5 reviews or mixed ratings |
| **2** | Has website or outside target niche |
| **1** | Wrong ICP · skip |

---

## ICP (Ideal Customer Profile)

- **Industries:** Plumbing · Roofing · HVAC · Electrical · Handyman
- **Revenue range:** $100K–$2M/year
- **Website status:** None or expired
- **Location:** Colorado Springs, Denver, Aurora (expanding)
- **Owner type:** Solo operator or small team

---

## Tech Stack

- **Scraping:** Apify — Google Maps Extractor
- **Qualification:** Claude API (Anthropic)
- **Storage:** Google Sheets CRM — Leads tab
- **Alerts:** Slack webhook → #leads
- **Orchestration:** n8n Cloud — `Apify → CRM Import` workflow
- **Interface:** [CartierHQ](https://github.com/cartiercreative8-art/cartier-hq) — CRM + Hermes tabs

---

## Output Format (CRM Row)

```
Date Added     | 05/19/2026
Business Name  | DeWalt Plumbing Services
Phone          | (719) 233-3210
Industry       | Plumber
City           | Colorado Springs
Lead Source    | Atlas — Google Maps
Website Status | No Website
Google Rating  | 4.2 stars, 6 reviews
Lead Score     | 3
Status         | In Progress
Follow Up Date | 05/21/2026
```

---

## Part of CartierOS

Atlas feeds leads directly into the [CartierOS](https://github.com/cartiercreative8-art/cartier-os) automation pipeline and [Jarvis Agent Core](https://github.com/cartiercreative8-art/jarvis-agent-core).
