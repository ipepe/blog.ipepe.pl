---
title: "Find 10 most commonly changed files in git repo"
categories: ["git"]
date: "2020-02-10"
---

```
git log --pretty=format: --name-only | sort | uniq -c | sort -rg | head -10
```