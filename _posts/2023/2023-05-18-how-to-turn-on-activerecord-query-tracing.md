---
title: "How to turn on ActiveRecord query tracing"
categories: ["ruby", "rails", "activerecord"]
---


Sometimes You need to see all SQL queries that are executed by ActiveRecord. There is built-in method and gem for that.

```ruby
# config/initializer/active_record_tracing.rb
if Rails.env.development?
  ActiveRecord::Base.verbose_query_logs = true
  # or 
  ActiveRecordQueryTrace.enabled = true # https://github.com/brunofacca/active-record-query-trace 
end
```