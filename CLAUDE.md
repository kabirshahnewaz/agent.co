# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is a **deliverables repository for a marketing/research agency** (WebShapers Agency), not a software project. It has no build system, package manager, tests, or application code. The tracked content is a set of **standalone HTML intelligence reports** produced for the client **agen.co** — an AI-agent security/governance company — based on Reddit market research.

Current reports (filenames are kebab-case and mirror the shared page-nav menu labels):
- `overview.html` — "Overview": landing page summarizing the whole Reddit intelligence suite.
- `roadmap.html` — "Roadmap": actionable Reddit marketing roadmap.
- `competitive-analysis.html` — "Competitive Analysis": named-competitor competitive intelligence.
- `market-analysis.html` — "Market Analysis": category-wide market intelligence on AI agent security.
- `subreddit-mapping.html` — "Subreddit Mapping": subreddit priority map, audience sizing, and targeting.

Every report carries an identical global page-nav strip (`.gnav`) at the top of its sticky header that
cross-links all five pages; the current page's link gets `class="active"`. When adding or renaming a
report, keep the filename kebab-case, matching its menu label, and update the `.gnav` block in every file.

## Report conventions (follow these when creating or editing reports)

Each report is a **single self-contained `.html` file** — no shared CSS/JS, no build step. Open directly in a browser to view.

- All styling lives in one inline `<style>` block per file. There is no external stylesheet to reuse; each new report copies and adapts the design system from an existing one.
- Typography: Google Fonts **Inter** (UI/body) and **JetBrains Mono** (data/mono), loaded via `<link>` to `fonts.googleapis.com`. These are the only external dependencies — everything else is inlined, so the fonts fall back gracefully offline.
- Data is embedded directly in the HTML (tables, cards, charts as inline SVG/CSS). Reports are point-in-time snapshots, not live dashboards.
- Keep the visual language consistent across reports for the same client (shared color palette, typography, card/section layout). When making a new agen.co report, mirror the structure of the existing files rather than inventing a new look.

## How the underlying data is gathered

Reports are built from Reddit research produced by the agency's skills and MCP tooling, not from code in this repo:

- **`reddit-keyword-audit`** skill — scrapes 300–500 posts for a keyword/niche and writes CSV + summary to `~/reddit-agency/clients/<client-name>/data/`.
- **`reddit-post-analyzer`** skill — analyzes a single Reddit post URL into a marketing report (sentiment, themes, pain points, engagement).
- **Apify MCP** (`mcp__apify__*`) — Reddit/web scraping Actors that back the audits.

When asked to "audit", "research Reddit", or "analyze a post" for agen.co (or another client), reach for these skills first. The HTML files in this repo are the presentation layer built on top of their output.
