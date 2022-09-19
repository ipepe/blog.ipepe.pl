---
title: "Top 11 ways to speed up Rails app"
categories: ["ruby","ruby-on-rails","programming","optimization"]
---


## 1. goldiloader or ar_lazy_preload
Rails for a long time now has problem with N+1 queries. There were many attempts to merge PR automatic eager loading of relationships into Rails codebase but without much success. I recommend using these gems to solve this problem. 

## 2. rack deflater = gzip compression of http responses
```ruby
# config/application.rb
require_relative "boot"
require "rails/all"
Bundler.require(*Rails.groups)

module MyRailsApp
   class Application < Rails::Application
      config.middleware.use Rack::Deflater # thats all
   end
end
```

## 3. bootsnap
Bootsnap changes how Ruby interpreter loads code. It caches some files in preprocessed results and this way, Rails app can load faster.

## 4. rubocop-performance
Rubocop performance checks if Your code is written correctly from performance stand point of view. It is a good idea to use this gem to check your code and fix suboptimal constructions.

## 5. ActiveRecord.pluck or ActiveRecord.distinct.pluck
I often see constructions that want to gather User's emails from database. To do this, it's good to not instatiate User class objects but to just ask database for strings directly and save CPU and Memory usage altogether.

## 6. Render Partials Properly
Often times developers write partials code like any other business logic, which might be suboptimal, for instance iterating over array in parial is really slow. To speed it up it's good to use collection construction:


Good:
```rhtml
<%= render partial: "events/event", collection: events, as: :event %>
```

Bad:
```rhtml
<% events.each do |event| %>
  <%= render partial: "events/event", locals: { event: event } %>
<% end %>
```

## 7. Use performant pagination tool like `pagy`, otherwise `will_paginate` or `kaminari` will slow down your app
There is big boom recently on using performant pagination gems and I think `pagy` is pretty good candidate for improving paging performance.

## 8. <https://github.com/rubymem/bundler-leak>
Sometimes Your rails application is slow and it's not your team's fault. It might be because of memory leak in dependecies. This tool will help You find out if Your dependency gems are slow and leaking memory.

## 9. Use fast json serialization with <https://github.com/ohler55/oj>
JSON serialization is big topic in Ruby world, there are many tools and many approaches to serializing to JSON. I recommend `oj` but only if You mearue actual performance boost, if not search for other JSON generating implementations both builtin in ruby and external libraries.

## 10. Use `counter_cache` when needed
Many junior and mid developers miss this functionality in Rails which might be useful in optimizing counter queries on relations.

If You want to level up Your counter cache game check out: <https://github.com/magnusvk/counter_culture>

## 11. Test only what changed recently: <https://toptal.github.io/crystalball/>
Crystalball is pretty amazing tool that uses code coverage to determine which test covers code of which files. This way if You have pretty big test suite that takes a lot of time to process, crystallball will check only files that are actually affected.

## BONUS: Stub paperclip/http requests or anything else that is slowing down Your tests
I recently optimized my tests in project by stubing paperclip `convert` behaviour and `post_process` behaviour. This way I can test my code without any paperclip dependencies and it runs REALLY fast. When needed this stub can be turned off on per test basis and feature can be covered appropiately.

