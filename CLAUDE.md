# Forge QC Dashboard

Reusable QC punchlist dashboard backed by Supabase. Used across all Forge projects.

## How It Works

Single `index.html` hosted on GitHub Pages. Fully dynamic — loads all data from Supabase based on URL parameters. No build step.

## Usage

```
https://trevorforge.github.io/forge-qc-dashboard/?project=wcc&date=2026-04-02
```

### URL Parameters

| Param | Required | Description |
|-------|----------|-------------|
| `project` | Yes | Project code (e.g., `wcc`, `irwd`, `yardtopia`) |
| `date` | Yes | Audit date (YYYY-MM-DD) |
| `supa_url` | No | Supabase URL (defaults to Forge instance) |
| `supa_key` | No | Supabase anon key (defaults to Forge instance) |

## Supabase Schema

Table: `qc_findings`

| Column | Type | Description |
|--------|------|-------------|
| id | serial | Auto-increment PK |
| finding_id | text | e.g., CONTENT-001 |
| project | text | Project code |
| audit_date | date | When the audit ran |
| severity | text | critical, warning, info |
| team | text | content, links, visual, ux, accessibility, seo, custom |
| page | text | URL path |
| element | text | CSS selector or description |
| description | text | What's wrong |
| suggested_fix | text | How to fix |
| status | text | open, approved, in_progress, fixed, needs_review, no_fix_needed, wontfix, deferred |
| notes | text | Decision notes |
| actor | text | Who made the last change |
| created_at | timestamptz | Auto |
| updated_at | timestamptz | Auto |

## For Claude Instances

When running QC fixes, update Supabase:
- Set `in_progress` when starting
- Set `fixed` when committed
- Set `needs_review` if uncertain
- Always set `actor` to your instance name
