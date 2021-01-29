---
title: Single file ruby script with library dependecies
categories: programming ruby
---

I often need to write a single file with external library dependecies for quick conversion or transforming of data. Heres a starter template:


```ruby
begin
  require 'bundler/inline'
rescue LoadError => e
  $stderr.puts 'Bundler version 1.10 or later is required. Please update your Bundler'
  raise e
end

gemfile(true) do
  source 'https://rubygems.org'

  gem 'activesupport'
end

require 'active_support/all'

```