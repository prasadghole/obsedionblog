---
title: "Whats in C Object name?"
date: 2021-03-21
tags: [programming]
description: "C objects names to avoid "
publish: true
---

# C Objects Naming
Although we know the common restrictions on naming identifiers like it should not start with number. There are some subtle
conventions we need to know. In this post I will note down those along with reasons behind these.

# Underscore
C compiler will not complain if we name identifiers starting with underscore, but it can create issues with portability
as C standard reserve the use of it by for naming new additional C keywords. Like 
```
_Bool
```

This is a new datatype introduced by C99 standard. Identifier starting with underscore followed by Capitol letter or another
underscore can or will be reserved keyword in future.

# _t (Underscore t)
When we define our own typedefs generally we follow the conventions of using postfix **underscore t**
We should avoid this as C standard reserves all the identifiers matching patterns 

```
int[0-9a-z_]_t

uint[0-9a-z_]_t

```
