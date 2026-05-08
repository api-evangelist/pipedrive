# Pipedrive (pipedrive)

Pipedrive is a sales CRM and pipeline management tool focused on small and mid-market teams. The Pipedrive REST API exposes deals, persons, organizations, activities, leads, products, pipelines, stages, mail, calls, files, notes, users, permissions, filters, goals, subscriptions, and webhooks.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/pipedrive/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=pipedrive-api-evangelist&utm_content=repo)

## Type

- **x-type:** company

## Tags

CRM, Sales, Pipeline Management, SaaS, Small Business

## Timestamps

- **Created:** 2026-05-08
- **Modified:** 2026-05-08

## APIs

| API | Tags |
|---|---|
| Pipedrive Deals API | Deals, Pipeline |
| Pipedrive Leads API | Leads |
| Pipedrive Persons API | Persons, Contacts |
| Pipedrive Organizations API | Organizations, Companies |
| Pipedrive Activities API | Activities, Tasks, Calendar |
| Pipedrive Pipelines API | Pipelines |
| Pipedrive Stages API | Stages |
| Pipedrive Products API | Products, Catalog |
| Pipedrive Notes API | Notes |
| Pipedrive Files API | Files, Attachments |
| Pipedrive Mailbox API | Mailbox, Email |
| Pipedrive Calls API | Calls, Telephony |
| Pipedrive Users API | Users, Seats |
| Pipedrive Permissions API | Permissions, Roles, Groups |
| Pipedrive Filters API | Filters, Saved Views |
| Pipedrive Goals API | Goals, Forecasting |
| Pipedrive Subscriptions API | Subscriptions, Recurring |
| Pipedrive Projects API | Projects, Delivery |
| Pipedrive Custom Fields API | Custom Fields, Metadata |
| Pipedrive Webhooks API | Webhooks, Events |
| Pipedrive Marketplace App API | Marketplace, OAuth, Apps |

## Plans

- **Essential:** $14/seat/month
- **Advanced:** $34/seat/month
- **Professional:** $49/seat/month
- **Power:** $64/seat/month
- **Enterprise:** $99/seat/month
- **Add-ons:** LeadBooster, Web Visitors, Projects, Smart Docs, Campaigns
- API token-budget multiplier scales 1x (Lite) → 7x (Ultimate)

## Rate Limits — Token Budget Model

- **Daily token budget:** 30,000 × plan multiplier × seats (+ top-ups)
- **Token costs:** single GET 2 / list GET 20 / update 10 / search 40
- **Per-user burst:** 2-second window (varies by plan)
- 429 returned when the daily budget is exhausted

## Common Properties

- [Website](https://www.pipedrive.com/)
- [Documentation](https://developers.pipedrive.com/)
- [API Reference](https://developers.pipedrive.com/docs/api/v1)
- [Pricing](https://www.pipedrive.com/en/pricing)
- [Status](https://status.pipedrive.com/)
- [Plans](plans/pipedrive-plans-pricing.yml) — API Commons Plans 0.1
- [Rate Limits](rate-limits/pipedrive-rate-limits.yml) — API Commons Rate Limits 0.1
- [FinOps](finops/pipedrive-finops.yml) — FOCUS-aligned FinOps Framework 1.0

## Artifacts

| Artifact | Path |
|---|---|
| Plans | `plans/pipedrive-plans-pricing.yml` |
| Rate Limits | `rate-limits/pipedrive-rate-limits.yml` |
| FinOps | `finops/pipedrive-finops.yml` |

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
