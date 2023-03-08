---
title: "Automatic Fix script to find broken migrations"
categories: ["rails", "database"]
---

I recently needed to find which migration broke `rails db:migrate:reset` and because there were hundreds of them, I wrote this simple script to run `db:migrate:reset` and remove migrations one by one from the end and find which one is last working one: 

```ruby
require 'open3'
loop do
  process = nil
  process_output = []

  ::Open3.popen2e(
    'bundle exec rake db:migrate:reset RAILS_ENV=test DISABLE_DATABASE_ENVIRONMENT_CHECK=1'
  ) do |_input, stdout_and_stderr, wait_thr|
    process = wait_thr
    io = stdout_and_stderr
    f = IO.select([io])[0][0]
    process_output.push f.readline until f.eof?
  end
  exit_status = process.value.exitstatus.to_i
  puts("Exit status: #{exit_status}")
  if exit_status != 0
    last_migration_file = process_output.reverse.detect do |line|
      line.include?('db/migrate/')
    end

    last_migration_file = last_migration_file.split(':').first

    if File.exist?(last_migration_file)
      puts("Removing last migration file: #{last_migration_file}")
      system("rm #{last_migration_file}")
    else
      puts("Parsing error: #{last_migration_file}")
      exit(1)
    end
  end
end
```