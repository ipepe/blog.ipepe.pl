---
title: "How to turn on ActiveRecord query tracing"
categories: ["ruby", "rails", "activerecord"]
---

When working with ActiveRecord in Ruby on Rails, it can be helpful to see all SQL queries that are executed. This can help with debugging and optimizing your application. In this post, we'll show you how to turn on ActiveRecord query tracing.

### Built-in Method

Rails provides a built-in method to turn on query tracing. You can do this by setting the `verbose_query_logs` option to `true` in your `config/application.rb` file:

```ruby
# config/application.rb
config.active_record.verbose_query_logs = true
```

This will log all SQL queries to your console.

### Gem

Alternatively, you can use the `active-record-query-trace` gem to turn on query tracing. This gem provides more detailed information about the queries that are executed.

To use the gem, add it to your Gemfile:

```ruby
# Gemfile
gem 'active-record-query-trace'
```

Then, enable query tracing in an initializer file:

```ruby
# config/initializers/active_record_query_trace.rb
if Rails.env.development?
  ActiveRecordQueryTrace.enabled = true
end
```

This will log all SQL queries to your console, along with information about the source of the query (e.g. file name and line number).

### Conclusion

By turning on ActiveRecord query tracing, you can get a better understanding of the SQL queries that are executed by your application. This can help you identify and fix performance issues, as well as debug any issues that arise.