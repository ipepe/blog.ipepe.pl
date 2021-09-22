---
title: Lessons from biggest Rails monolith
categories: rails
---

Cookpad is/was one of biggest rails monoliths and it is one of most succesful monoliths in Rails.

This will be my take on most interesting tools and solutions to problems I found in presentation slides at <https://speakerdeck.com/a_matsuda/the-recipe-for-the-worlds-largest-rails-monolith>

Bear in mind this presentation was published on 5th of March 2015.

## Into - how big is this monolith?
 * 276 gems
 * 1732 Model classes
 * 518 Controller classes
 * 50 million unique users per month
 * 15 thousand requests per second
 * 300 rails server instances
 * 30 separate databaseses (1141 lines in config/database.yml) 
 * 50 developers
 * 2000 commits per month
 * 10 deploys per month

## Performance requirements
 * HTML request less than 200msec
 * API request less than 80msec

## Scaling solution

At peak to handle all traffic there needs to be 300 rails servers, but that is not required all the time. There is dynamic scaling tool that increases number of rails server instances.

Custom in-house tool was built to manage scaling and be compatibile with deployments: `cookpad-autoscale`
 * Locks auto-scaling when deploying
 * Locks deployment when auto-scaling
 * Similiar to Amazon AutoScaling

## Deployment solution

Capistrano is good for small-medium projects, but when reaching big scale - time matters.

Cookpad team created `sorah/mamiya` to deploy their code. Mamiya uses Serf for orchestration, Gossip protocol instead of SSH. Collaborates with the repo, the CI server, and the auto-scaler.

Scaling 300 rails servers takes about one minute. More than 10 times faster than Capistrano.


## Database scaling solution

Cookpad team created their own ActiveRecord adapter: `eagletmt/switch_point`

It has very simple master / slave connection switch

Less monkey-patching to ActiveRecord core.

Code example:

```ruby
SwitchPoint.configure do |config|
  config.define_switch_point :main,
                             readonly: :"#{Rails.env}_main_slave",
                             writable: :"#{Rails.env}_main_master"
end

class Recipe < ActiveRecord::Base
  use_switch_point :main
end


Recipe.with_readonly { Recipe.find(id) }
Recipe.with_writable { Recipe.create! }
```

## Scaling capybara tests

How to scale tests that take 5 hours to complete?

Goal: Tests should finish within 10 minutes

Solution: Distributed RSpec executor (`rrrspec`)
 * scp local source code to a powerful remote test runner
 * run them in parallel

## Database cleaner is too slow

With 1000 database tables database cleaner is really slow. Why? Because it deletes from all tables.

Solution: Delete only from tables that were used in test case (`amatsuda/database_rewinder`)

## Database migrations

Cookpad team does not use ActiveRecord Migrations. They created in-house `Schemaless` tool: `winebarrel/ridgepole`

It maintains database schema in one Ruby DSL file and determines what needs to change based on current databse state vs declared schema.

## How to avoid conflicts with 50 developers working on core buisness

In-house prototyping solution: `cookpad/chanko`

Chanko provides a simple framework for rapidly and safely prototyping new features in your production Rails app, and exposing these prototypes to specified segments of your user base.

`app/units/example_unit` - put here whole MVC

```
$ rails generate chanko:unit example_unit
      create  app/units/example_unit
      create  app/units/example_unit/example_unit.rb
      create  app/units/example_unit/views/.gitkeep
      create  app/units/example_unit/images/.gitkeep
      create  app/units/example_unit/javascripts/.gitkeep
      create  app/units/example_unit/stylesheets/.gitkeep
      create  app/assets/images/units/example_unit
      create  app/assets/javascripts/units/example_unit
      create  app/assets/stylesheets/units/example_unit
```

```ruby
# app/controllers/users_controller.rb
class UsersController < ApplicationController
  unit_action :example_unit, :show

  def index
    invoke(:example_unit, :index) do
      @users = User.all
    end
  end
end
```

## How to upgrade rails version?

Solution: HTTP shadow proxy server (`cookpad/kage`)

Cookpad runs the actual user requests on shadow servers and compares HTML response body on shadow vs live server


Sources:
 * <https://speakerdeck.com/a_matsuda/the-recipe-for-the-worlds-largest-rails-monolith>