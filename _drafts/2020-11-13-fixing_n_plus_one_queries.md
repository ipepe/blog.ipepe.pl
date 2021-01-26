# Fixing n+1 queries

Sometimes when developing serializers we introduce n+1 queries. To track and fix them, it's recommended to use bullet gem.

At current project state, it's not reasonable to have bullet gem turned on constantly, but when needed, You can add 

`gem 'bullet'` to Gemfile

and 

```ruby
  config.after_initialize do
    Bullet.enable = true
    Bullet.rails_logger = true
    Bullet.raise = true
  end
```

to `development.rb` or `test.rb` - depends where You are trying to track down n+1

Also, when bullet reports `AVOID eager loading detected` it should be ignored as serialiers sometimes require specific attributes, sometimes not.
