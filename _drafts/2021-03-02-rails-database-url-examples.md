---
title: Rails DATABASE_URL examples
categories: ruby
---


## Sqlite in memory
```
DATABASE_URL=sqlite3::memory:
```

`database.yml`
```yaml
test:
  adapter: sqlite3
  database: ":memory:"
```
