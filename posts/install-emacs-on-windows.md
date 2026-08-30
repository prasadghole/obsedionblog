---
title: "Installing spacemacs on windows"
date: 2021-01-26
tags: [development, vim]
publish: true
---

# Installing spacemacs on windows
Once we install vanilla emacs from gnu website we want to do  little  twick for  running emacs configuration when  we
run runemacs.exe command.

We need to find out where is  emacs startup home directory path.  

## Finding  startup directory 

Check user  emacs directory 
```bash
CTRL-H  v 
```
Enter variable name
```bash
user-emacs-directory
```


## Cloning spacemacs configuration 
When ever emacs starts it looks for startup directory in  user emacs directory found above.  We will get 
that configuration directly from github.com.


```bash
git clone https://github.com/syl20bnr/spacemacs C:\%USERPROFILE%\appdata\roaming\.emacs.d
```

### Job well done
Enjoy
