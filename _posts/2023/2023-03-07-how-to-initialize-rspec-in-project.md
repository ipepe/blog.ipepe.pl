---
title: "How to initialize RSpec in project"
categories: ["ruby", "rspec"]
---

There are mostly two ways to initialize RSpec in project. One for pure Ruby projects and one for Rails projects.

## Pure Ruby project

To initialize RSpec in pure Ruby project, you need to add `rspec` gem to your `Gemfile` and run `bundle install` command or simply use `bundle add rspec`

Then you need to run `rspec --init` command to initialize RSpec in your project.

## Rails project

To initialize RSpec in Rails project, you need to add `rspec-rails` gem to your `Gemfile` and run `bundle install` command or simply use `bundle add rspec-rails`

Then you need to run `rails generate rspec:install` command to initialize RSpec in your project.

## Sources:
 * <https://www.youtube.com/watch?v=pKSvbIslhZc>

