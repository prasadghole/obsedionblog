---
title: "Git in a box"
date: 2019-08-26
tags: [development, git]
publish: true
---

# Git in a box 
Github is certailnly a good source of keeping master copy of your decentralized git repo. But in some 
scenario project thing it would be much better to have git repository as portable copy.This is where 
git bare repository helps.

## Bare repository
A bare repository is one without working copy. We can push or pull our changes to/from this repo. We
can keep this repository portable and handy. Can be mount on shared drive and your github is done.
```C
git init --bare 

```
## Using bare repository
We can push existing repo to this file based repository similar to remote repository.

git remote add origin <path of bare repo> 

git push -u origin master

We can clone this bare repository similar to our github repo
git clone <path of bar repository> <clone directory>
