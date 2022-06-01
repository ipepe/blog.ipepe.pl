---
title: "Find 10 most commonly changed files in git repo"
date: "2022-02-10"
categories: ["git"]
---

```
git log --pretty=format: --name-only | sort | uniq -c | sort -rg | head -10
```