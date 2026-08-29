# obsedionblog vault

Markdown second-brain, replacing the old Emacs org-mode + Hugo workflow. This vault is the
**private** source of notes; the public site is built from it by a separate repo,
[obsedionblog-quartz](https://github.com/prasadghole/obsedionblog-quartz), and published to
[prasadghole.github.io](https://prasadghole.github.io).

## Folder layout
- `posts/` — blog posts, published or not (controlled by frontmatter, see below)
- `drafts/` — work in progress, never built into the site regardless of frontmatter
- `clippings/` — saved web pages (via Obsidian Web Clipper)
- `attachments/` — images/screenshots referenced by notes
- `templates/` — note templates
- `index.md` — the site's homepage content

## Writing a new blog post

1. In Obsidian, create a new note under `posts/`.
2. Insert the blog post template: **Ctrl/Cmd+P → "Insert template" → `blog-post`**
   (first time only: **Settings → Core plugins → Templates → Template folder location** →
   set to `templates`).
3. Fill in the frontmatter and write the post. Screenshots/images: paste directly into the
   note — Obsidian saves them into `attachments/` and links them automatically.
4. To make a note public, set `publish: true` in its frontmatter (see below). Leave it
   `false` (or just don't touch it) to keep working on it privately.
5. Commit and push the vault repo. The site does **not** update automatically — see
   "Publishing" below.

### The `publish` frontmatter flag
This is the only thing that controls what goes live:
```yaml
---
title: "My post title"
date: 2026-08-29
tags: [programming]
publish: true   # false (or omitted) = stays private, even if committed
---
```
A note can be committed to this repo — and even sit in `posts/` — without ever appearing on
the site, as long as `publish` isn't `true`. `drafts/`, `clippings/`, `templates/`, and
`.obsidian/` are excluded from the site build entirely regardless of frontmatter.

## Template
`templates/blog-post.md`:
```yaml
---
title: "{{title}}"
date: {{date}}
tags: []
description: ""
publish: false
---

## Summary

## Notes
```
- `title` — shows as the page title and in link previews
- `date` — used for sorting and display
- `tags` — shown on the post and used for the site's tag pages
- `description` — short summary used for SEO/link previews (optional but recommended)
- `publish` — defaults to `false` so nothing goes live by accident

## Publishing to the web
This repo only holds content — building and deploying the site happens in
[obsedionblog-quartz](https://github.com/prasadghole/obsedionblog-quartz):
1. Commit and push your changes here.
2. In `obsedionblog-quartz`: `git submodule update --remote content`
3. Run `scripts/publish.nu` (Nushell) or `scripts/publish.sh` (Bash) — builds the site and
   pushes it to `prasadghole.github.io`.

## Other tools
- **obsidian.nvim** — for CLI/vim-motion editing of this same vault from Neovim
- **Obsidian Web Clipper** — saves web pages as markdown into `clippings/`
