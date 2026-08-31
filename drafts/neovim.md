---
title: "Setting up neovim on windows"
date: 2023-06-09
tags: []
publish: false
---

# Package manager
I use vimplug as plugin manager.
```shell
iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim | ni "$env:LOCALAPPDATA\nvim\autoload\plug.vim" -Force
```

# Configuration Directory
This is different than traditional vim
```shell
$HOME\AppData\Local\nvim\init.vim
```


# Plugins for completion
```vim
call plug#begin('$HOME/.vim/plugged')

" Plugins
Plug 'dense-analysis/ale'          " Asynchronous Lint Engine (ALE)
Plug 'neoclide/coc.nvim', {'branch': 'release'}   " CoC (Conquer of Completion)

call plug#end()
  
```


## Coc-pyright
Initially I tried coc-python but it seems not working on python 3.11. Hence
I moved to pyright.
