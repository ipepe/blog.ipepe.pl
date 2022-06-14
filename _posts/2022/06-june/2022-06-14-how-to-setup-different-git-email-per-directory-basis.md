---
title: "How to setup different git email per directory basis"
categories: ["git"]
---

Sometimes it is necessary to have different git email per directory basis. 

This is configuration example how to do it:

In`~/.gitconfig`:
```
[user]
  name = Bruce Wayne
  email = bruce.wayne@example.org
[includeIf "gitdir:~/projects/gotham/"]
  path = ~/Projects/gotham/.gitconfig
[core]
  editor = vim
```

In `~/projects/gotham/.gitconfig`:
```
[user]
  name = Batman
  email = batman@example.org
```