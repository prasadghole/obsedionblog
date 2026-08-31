---
title: "Pipenv uncomplicated package manager for python"
date: 2022-08-27
tags: []
description: "Creating and managing virtual environments in python"
publish: false
---

# Installation
Well we need pip only at startup.
```shell
pip install pipenv
```

# Usage
Starting blank virtual environment 
As I using both python2 and 3 its better to specify version

```shell
pipenv shell --three
```

Once created we can verify current installed pip packages
```shell
pipenv graph
```

This should return empty in case we start from fresh python install
else will show packages installed in base interpreter from which
this new environment is created.
