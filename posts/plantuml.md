---
title: "Plantuml"
date: 2021-02-05
tags: [everthing is code, mouseless]
description: "Plantuml tool"
publish: true
---

# Plantuml
Plantuml is markup language for software diagrams specifically UML. Especially for 
programmers it natural extension of drawing diagrams as coding. 

![Plantuml Website](https://plantuml.com/)

## Why Plantuml

### Mouseless
I am trying to minimise my mouse uses. With the help of tools we can draw and view
diagrams without touching mouse.

### Everything is text
Many UML drawing tools (MS visio) store diagrams in internal proprietary binary
format.  To view and modify we need tools installed. Most of these tools are
very expensive.
Writing Plantuml markup is almost similar to writing C code.

### Source Control
As diagrams are described in text format. I can store them in git and track
changes easily. In case of drawing tools being binary simple version control
diffs are not sufficient.

### Integration with other tools
Plantuml library mainly provide backend framework and easily integrate with various
text editors and IDE. I used it with 
- Visual Studio Code
- Eclipse
- Confluence
- Emacs (need to check spacemacs support)

### Lightweight
It uses simple java libraries graphviz.
