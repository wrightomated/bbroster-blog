# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is the changelog/news blog for **BB Roster** (a Blood Bowl roster-building tool at https://bbroster.com), built with the [Hugo](https://gohugo.io) static site generator. It is published at https://blog.bbroster.com/. Content is almost entirely Markdown posts announcing product updates; there is very little custom code.

## Commands

- `hugo server -D` — run local dev server with drafts visible (posts default to `draft: true`)
- `hugo server` — local dev server, published posts only
- `hugo new posts/<slug>.md` — scaffold a new post from `archetypes/default.md`
- `hugo` — build the static site into `public/`

There is no test/lint/build tooling beyond Hugo itself; `public/` and `resources/` are gitignored generated output.

## Architecture

- **`config.yaml`** — site config. `theme: paper-mod` selects the active theme; `defaultTheme: auto` enables light/dark auto-switching. The main menu and `baseURL` live here.
- **`content/posts/*.md`** — the blog posts. Each has front matter with `title`, `date`, `draft`, and `tags` (e.g. `["News", "Blood Bowl 2025"]`, `["Updates"]`). New posts start `draft: true` — flip to `false` to publish. Posts can embed Hugo shortcodes such as `{{< youtube <id> >}}`.
- **`content/*.md`** — standalone pages (`private-policy.md`, `terms-of-use.md`).
- **`themes/`** — both `paper-mod` and `paper` are git **submodules**. `paper-mod` (hugo-PaperMod) is active. After cloning, run `git submodule update --init --recursive` or themes will be missing. Do not edit theme files directly; override via `assets/` and `layouts/` instead.
- **`assets/css/extended/home-info.css`** — PaperMod's convention for custom CSS overrides that get bundled into the theme build.
- **`static/`** — served at site root as-is: `images/` (post images), `favicon.ico`, and Google site-verification HTML files.

## Authoring guidelines

Posts are written by the site's solo developer. Match that voice:

- **First person, personal.** "I've added...", "I want to clarify...". Use "we" only when it reads naturally. It's a developer talking to players, not a company issuing a press release.
- **Casual and warm.** Contractions, plain words, the occasional exclamation point. Blood Bowl flavor and light humor are welcome (see `welcome-gnome.md`, `journeymen-types.md`) but never forced.
- **Short.** Most posts are a few sentences to a few short paragraphs. Say what changed and how to use it, then stop. Use `##` headings and numbered steps only for longer how-to posts (see `saving-your-rosters.md`).

Avoid these tells that read as AI-written:

- **No antithesis/"not X, it's Y" constructions** ("This isn't just a tweak, it's a revolution").
- **No em dashes.** Rephrase into separate sentences or use commas/parentheses.
- **No hyperbole or marketing filler** ("game-changing", "seamless", "revolutionize", "we're thrilled to"). State the change plainly.
- **No rule-of-three lists** for their own sake, and no summary paragraph that restates what was just said.

## Notes

- Create posts with `hugo new posts/<slug>.md` so the `date` is stamped from the author's current system time. The offset will reflect the local timezone (`+10:00` AEST, or `+11:00` during daylight saving) — that's expected, no need to normalize it.
- To customize the theme, prefer PaperMod's override mechanism (matching file paths under `assets/`/`layouts/`) rather than modifying the submodule.
