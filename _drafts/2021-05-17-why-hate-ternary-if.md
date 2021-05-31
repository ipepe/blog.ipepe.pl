---
title: Why I hate ternarny if in Ruby
categories: ruby
---


## Example 1
```ruby
# File activerecord/lib/active_record/base.rb, line 2916
  def create_or_update
    raise ReadOnlyRecord if readonly?
    (new_record? ? create : update) != false
  end
```

## Example 2

```ruby
resp = request ? resp.success? ? resp.body : { error: 404 } : false
```
