---
name: readme-style
description: Write GitHub/GitLab READMEs in a clean, understated open-source style — badge hero, honest feature prose, explicit limitations. Use when writing or improving a README or repo landing docs.
---

Style only: layout is whatever the project needs. These govern how it reads.

## Voice
Understate: "still growing", "work-in-progress", "might be useful for". Never
"blazing-fast", "revolutionary", "cutting-edge", "seamlessly". No superlatives, no
exclamation marks, no marketing em-dashes.
Plain verbs, present tense, second person for instructions. Short sentences, short
paragraphs. Answer "should I spend ten minutes on this", then stop. Match the repo's
US/UK spelling.

## Honesty

Name what does not work — a limitations section is the trust signal, never soften it.
Verify before writing: read `package.json`/`composer.json`/`pyproject.toml`/`Cargo.toml`,
`LICENSE`, CI config. Never invent versions, licenses, badges, stars, benchmarks,
feature names, URLs, or screenshot paths; unknown gets a visible placeholder plus a note.
Commands run in the order given; flag anything untested.

## Presentation

Badges: shields.io flat, one per line, each linked. Brand colour where known, `green`
for version/license, `555` neutral. Escape `-`→`%2D`, space→%20.
`https://img.shields.io/badge/<LABEL>-<VALUE>-<COLOR>?logo=<LOGO>&logoColor=white`
PHP 777BB4 · Laravel FF2D20 · MySQL 4479A1 · Docker 2496ED · Node 339933 · Python 3776AB ·
React 61DAFB · TypeScript 3178C6 · Go 00ADD8 · PostgreSQL 336791.

Tagline is a sentence, not a slogan, under ~90 chars. Headings sentence case and literal
("Manual installation"), not clever. Code blocks always carry a language, shell blocks
omit `$`. Inline `code` for paths, env vars, flags. Tables only for real grids.
Collapse optional/long content (alt installs, prerequisites, roadmaps) in
`<details><summary>` whose summary says what's inside. Images: relative paths, no `./`,
no encoded spaces; omit rather than link a dead path.

## Platforms

Badges and `<details>` work on GitHub and GitLab; heading anchors match on both.
GitLab strips `align` from `<div align="center">`, so centered blocks go left-aligned
there — accept it. Only use badge endpoints that exist (`/badge/`, `/npm/v/`, `/pypi/v/`).
