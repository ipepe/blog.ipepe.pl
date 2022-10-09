---
title: "My Rails setup"
categories: ["rails", "ruby", "programming"]
---

# 1. Autoload paths

```ruby
config.autoload_paths << Rails.root.join("app", "services")
config.autoload_paths << Rails.root.join("app", "tasks")
```

