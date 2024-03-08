---
title: "Vim: Inserting command output"
date: Tue Mar 05 16:45:16 -0500 2024
tags:
  - vim
---

Two ways.

From command mode:

```
:r!command
```

Or from insert mode, press `Ctrl-R`, then enter

```
=trim(system('command')
```
