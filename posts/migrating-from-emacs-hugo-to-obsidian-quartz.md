---
title: "Moving my blog off Emacs org-mode and Hugo"
date: 2026-08-30
tags: [meta, tooling]
description: "Why I replaced my Emacs org-mode + Hugo blogging setup with an Obsidian vault and Quartz, and what the migration actually took."
publish: true
---

## Summary

I've replaced my old blogging setup — writing in Emacs org-mode and publishing with Hugo — with
an Obsidian vault publishing through Quartz. This post is about why, and what the switch actually
involved.

## Notes

### Why move at all

Emacs org-mode had been my capture tool for years: programming notes, clippings from around the
internet, screenshots, and lately a growing pile of AI-generated markdown. The problem wasn't
org-mode's writing experience — it was everything around it. Emacs is single-threaded, and it
never really integrated with the rest of a modern capture workflow. Organizing and labeling notes
was entirely on me; there was no real second-brain layer doing that work.

What I wanted instead: a plain-markdown tool that handles organization itself (tags, backlinks),
that I can still drive from the keyboard with vim motions, that captures code/web clips/screenshots/
AI content without friction, and that still lets me publish to the web.

### What I landed on

- **Obsidian** for the vault itself — plain markdown files, wikilinks and backlinks built in, and
  `obsidian.nvim` so I can still edit from Neovim with vim motions when I want to.
- **Quartz** for publishing — a static site generator built specifically for markdown vaults like
  this one, rather than something I'd have to bend Hugo into shape for.

### The repo split

I initially had the vault and the Quartz engine merged into a single repo. That turned out to be
the wrong call once privacy became a real requirement: notes and drafts should stay private, but
the site engine and the published HTML are fine to be public. So the setup ended up as three repos:

- `obsedionblog` — the vault itself (private)
- `obsedionblog-quartz` — the Quartz engine, with the vault pulled in as a git submodule
- `prasadghole.github.io` — the actual published site, also pulled into the Quartz repo as a
  submodule, Hugo-`public/`-submodule style

A note only goes live if its frontmatter has `publish: true` — everything else (drafts, clippings,
templates) stays out of the build regardless.

### Two bugs worth remembering

Quartz wipes its output directory completely before every build. That's fine when the output
directory is disposable, but I was building straight into the `public/` submodule the first time,
and its `.git` is a *file* (a submodule gitlink), not a directory — so the build silently deleted
it and broke the submodule. Fix: always build into a throwaway folder and mirror it into `public/`
afterward, rather than building into `public/` directly.

The second one: GitHub Pages runs everything through Jekyll processing unless you tell it not to.
Without a `.nojekyll` file, my site's root URL was resolving to the RSS feed instead of the actual
homepage. Adding `.nojekyll` — and giving the vault a real `index.md` — fixed it.

### Where it stands now

Publishing is a two-step, manual process: push the vault, then run a publish script (I keep both
a Nushell and a Bash version) from the Quartz repo that builds the site and pushes the result. No
CI yet — that's the next thing to revisit, along with actually migrating the old org-mode archive
over.
