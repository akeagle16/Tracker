# CLAUDE.md — Project Tracker Repo

This repo is the single source of truth for Clay White's digital product portfolio. Clay is **Product Manager of the Digital Tools Portfolio** at VusionGroup — accountable for owners, commitments, and outcomes across workstreams, and one IC among several on hands-on work (select UI), not the default owner of every line. Track timelines by owner / commitment / outcome. The delivery team: **Eric** (backend / data pipeline), **Cristina** (frontend), **Zel** (beta + physical inspection), with Clay as PM. `tracker.json` holds all project state. Every Claude Code session in this repo follows the rules below.

## What lives here

- `tracker.json` — canonical state: projects, modules, milestones, blockers, carry-forwards, recurring deliverables, operating principles
- `docs/index.html` — static dashboard generated FROM tracker.json, published via GitHub Pages (build it on first session if it doesn't exist; same style family as Clay's other tools at claywhite3.github.io)

## Hard rules (never violate)

1. **Carry-forward items are never deleted.** They can only move to `status: "resolved"` with a `resolution` note and a resolution date. They appear in every weekly deliverable until resolved — this is intentional ("flag until nauseating").
2. **Every change to tracker.json gets a changelog entry** on the affected project: `{ "date": "YYYY-MM-DD", "entry": "what changed" }`.
3. **Always update `meta.last_updated`** when the file changes.
4. **Validate the JSON** (parse it) before committing. Never commit a broken tracker.
5. **After any tracker.json change, regenerate `docs/index.html`** so the dashboard never drifts from the data. When regenerating: replace ONLY the `TRACKER` constant in the `<script>` block with the current tracker.json contents. Never modify the markup or styles.
6. **Commit and push after every update — always directly to `main`. Never use branches or pull requests.** Commit message format: `tracker: <short description>` (e.g., `tracker: validation module complete`).
7. **Dates are commitments.** Never silently change a due date — if Clay moves one, log the old date and new date in the changelog entry.

## Status vocabulary

`done` · `on_track` · `at_risk` · `blocked` · `escalation` · `planning` · `not_started` · `in_progress`

## Commands Clay will use (treat these as workflows)

### "update: <plain-English status change>"
Parse it, edit tracker.json accordingly, add changelog entry, validate, regenerate dashboard, commit, push. Confirm in one short line what changed. Examples:
- "update: validation module shipped" → mark module done with today's date, advance next_milestone to Maintenance (7/3)
- "update: Jessie's data landed" → flip esl-maintenance-app to in_progress, clear the blocker, note the date

### "status" or "where am I"
Read tracker.json and give a tight readout: what's due in the next 7 days, what's blocked, what's at risk, weeks-open count on every carry-forward. No fluff.

### "friday" (weekly deliverables)
Generate both, drawing only from tracker.json:

1. **Leadership slide content** — Thaddeus standard: fits a single slide, **max 200 words**, delete unused boxes, relevance over completeness. Lead with what changed this week; always include open carry-forwards.
2. **Weekly recap email draft** — subject line exactly: `Weekly Recap | [Date] | Product Implementation`. SharePoint links as `[LINK]` placeholders. Structure: wins → in flight (with dates) → blocked/escalated → carry-forwards (with weeks open).

Apply the deployment-to-results principle in both: tie any performance claim to its deployment config ("this config = this performance = this cost"). Never report raw metrics without config context.

### "new project: <description>"
Add a project object following the existing schema. Ask only for: due date (if any), who it serves, blockers. Everything else defaults.

## Carry-forward mechanics

- `weeks_open` = full weeks since `opened`. Recompute whenever generating a status readout or weekly deliverables. (Open dates currently TBD — ask Clay to backfill, then compute.)
- Resolved items stay in the file under `status: "resolved"` for the record; they drop out of weekly deliverables after appearing once as "RESOLVED" with the resolution note.

## People map (for context in drafts)

- **Thaddeus** — SVP Product; sets leadership comms standards (the 200-word slide rule)
- **Nick** — Clay's direct manager; owns RMA/escalations (Blink ID)
- **Eric** — backend / data pipeline; owns the Validation pipeline (hardware-state → UI) and the QC data pull. His pipeline + post-6/22 bandwidth is the biggest shared portfolio dependency.
- **Cristina** — frontend; owns the Companion App add/delete Sections build
- **Titouan** — meets with Eric 6/16 re the Validation pipeline fix
- **Zel** — Companion App beta + physical inspection (Gen1 daily walks)
- **JB** — Site Survey Tool partner
- **Connor** — GT tool stakeholder; **Sean** — cross-functional
- **Jessie** — ESL data pull (gates ESL Maintenance App); **Emmanuel Amy, Rafael** — parallel Sainsbury's touchpoints
- **Tarik, Ramyaa, Peyton, Anderson** — extended team / contractors

## Products context

TopStock Rail is the flagship physical product (Walmart: 5 Gen1 stores, AR/TX). Captana is the computer-vision product (Sainsbury's: 4 UK stores). Clay's portfolio = the digital tools that enable these products. ESL = electronic shelf labels.

## Tone for generated deliverables

Direct, factual, no filler. Leadership artifacts favor relevance over completeness. Blockers and carry-forwards are stated plainly, never softened.
