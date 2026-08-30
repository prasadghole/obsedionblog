---
title: "Reveal Secrets"
date: 2021-02-02
tags: [emacs, publishing]
description: "Reveal.js links"
publish: true
---

# Reveal js
Converting daily notes to beautiful presentations made easy with reveal js integration. Configuration is also very simple but still there are some
tit bits to remember. Below are some of the links 

# Configuring emacs (spacemacs)
https://www.johbo.com/2017/presentations-with-org-mode.html

http://jr0cket.co.uk/2017/03/org-mode-driven-presentations-with-org-reveal-spacemacs.html

# About org mode
http://jr0cket.co.uk/2013/08/manage-dev-life-with-emacs-org-mode.html

https://orgmode.org/

# Publishing to Internet
http://jr0cket.co.uk/2014/01/share-your-revealjs-slides-on-github-pages.html

# Using Pandoc
```
pandoc --standalone -f org -t revealjs  TraingSlides.org -o out.html
```

As I may not use emacs/spacemacs on every machine Pandoc is right option to create revealjs output from org or markdown
document.
