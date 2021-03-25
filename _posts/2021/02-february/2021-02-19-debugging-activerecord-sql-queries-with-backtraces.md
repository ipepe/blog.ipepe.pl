---
title: Debugging ActiveRecord SQL Queries with Backtraces
categories: rails
---

## hijacking logger
 * `config.log_level = :debug`
 * `Rails.logger = Logger.new(STDOUT)`
 * `ActiveRecord::Base.logger = Logger.new(STDOUT)`

## verbose_query_logs

After running `ActiveRecord::Base.verbose_query_logs = true` in the bin/rails console session to enable verbose query logs and running the method again, it becomes obvious what single line of code is generating all these discrete database calls:
```
Article Load (0.2ms)  SELECT "articles".* FROM "articles"
↳ app/models/article.rb:5
Comment Load (0.1ms)  SELECT "comments".* FROM "comments" WHERE "comments"."article_id" = ?  [["article_id", 1]]
↳ app/models/article.rb:6
Comment Load (0.1ms)  SELECT "comments".* FROM "comments" WHERE "comments"."article_id" = ?  [["article_id", 2]]
↳ app/models/article.rb:6
Comment Load (0.1ms)  SELECT "comments".* FROM "comments" WHERE "comments"."article_id" = ?  [["article_id", 3]]
↳ app/models/article.rb:6
```

## active-record-query-trace

There is gem https://github.com/brunofacca/active-record-query-trace
