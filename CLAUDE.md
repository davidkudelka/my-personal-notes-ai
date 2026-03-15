# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

This is David Kudelka's personal Obsidian knowledge vault — a markdown-based personal knowledge management (PKM) system. It is not a software project with build/test/deploy pipelines. Content is written in standard Markdown and managed via Obsidian.

## Repository Structure

```
├── Finance/              — Investment portfolio, budget, taxes, finance books
│   └── Investment Portfolio Tracking.md   ← frequently accessed, most important file
├── Work/
│   ├── Crave/            — Crave food service project notes
│   ├── Productboard/     — Productboard company notes, ADRs, performance reviews
│   ├── Plextrac/         — Plextrac GraphQL project notes
│   └── Other/            — OAK'S LAB, job search, interviews, freelance
├── Learning/
│   ├── Tech/             — React, GraphQL, Relay, testing, system design notes
│   └── Books/            — Book notes (Composing Software series, PKM, productivity)
├── People/               — Mentoring notes, 1on1s, performance feedback
├── Personal/             — Health, habits, dog, travel, personal development
├── Daily notes/          — Daily journal entries by year (2024/, 2025/, 2026/)
├── Sloth app/            — Docker/Tailscale relay service on Raspberry Pi
├── Research UX/          — MVP research, cost analysis, project task tracking
├── Project feedback/     — Feedback documents on external projects
├── Therapy/              — Personal therapy session notes
└── Roam/
    └── david_kudelka_notes/
        └── Daily/        — Legacy Roam Research daily notes (2020–2024, 723 files)
```

## Key Files

- **Finance/Investment Portfolio Tracking.md** — Monthly portfolio snapshots since Feb 2023, actively updated around the 21st of each month. Has YAML frontmatter with tags.
- **Home page.md** — Top-level navigation hub.

## Content Conventions

- Notes use Obsidian wiki-links (`[[Note Title]]`) for internal linking.
- Daily notes follow `YYYY-MM-DD.md` format under `Daily notes/YYYY/`.
- `Roam/david_kudelka_notes/Daily/` is a read-only historical archive (Roam Research import, 2020–2024).
- Tags use YAML frontmatter (`tags:` list) in newer files, or inline `* tags: #tag` style in legacy Roam imports. Be consistent with the existing style of the file being edited.

## Key Projects Documented

- **Sloth app**: Relay service using Tailscale + Docker on a Raspberry Pi (`Sloth app/Basic Information.md` has maintenance commands and IPs).
- **UX Research project**: AI-powered screenshot tagging tool with Cloudflare R2, DigitalOcean, and Clerk (`Research UX/`).
- **Crave**: Food service startup (~2020–2021 era, archived in `Work/Crave/`).
- **Productboard**: Detailed technical work notes 2021–2023 in `Work/Productboard/`.
