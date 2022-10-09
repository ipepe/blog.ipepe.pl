---
title: "How to create parameterized rake task"
categories: ["ruby", "rake", "rails"]
---

I have a rake task that I want to parameterize. For example, I want to run it like this:

```bash
rake generate_previews[create_missing_only]
```

Code to create such task should look like this:
```ruby
desc 'Generate color covers for all parts'
task :generate_previews, [:create_missing_only] => [:environment] do |_, args|
  (Rails.logger = Logger.new(STDOUT))
    GeneratePreviewsTask.new(
        create_missing_only: args[:create_missing_only].to_s == 'create_missing_only',
        logger: (Rails.logger = Logger.new(STDOUT))
    ).process
end
````
