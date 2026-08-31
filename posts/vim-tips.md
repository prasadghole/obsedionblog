---
title: "Vim Tips"
date: 2019-07-29
tags: [development, vim]
publish: true
---

## Search in visual mode
Follow the steps:

  1. Select visual mode by V or select block or column by using CTRL_V 
  2. Press escape to exit visual mode
  3. Search ``/`` as you do for regular search

## Edit multiline together 
In various case I need to append or insert test at multiple lines like adding
semicolon at the end of lines. I followed below steps
1. CTRL+V to select block.
2. Press I to insert at start.
3. Type character at first line.
4. Escape and you will see same character is applied to all the selected lines.


![[attachments/vim-tips-vim1.gif]]

## Spell check 
### Add word to spell check dictionary
Vim stores good words in 'spellfile'. 
Place cursor on wrong word and press 

**zg**
