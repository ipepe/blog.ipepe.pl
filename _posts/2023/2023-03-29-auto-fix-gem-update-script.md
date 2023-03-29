---
title: "Auto fix gem update script"
categories: ["ruby", "devops", "programming"]
---

I recently needed to update all gems in my project and I wrote this script to do it so that it takes Gemfile.lock from other project and tries to install all gems that are compatibile with it.

```ruby
require 'open3'

gemfile_lock = <<-TXT
Gemfile.lock content
TXT


loop do
  File.write('Gemfile.lock', gemfile_lock)
  original_gemfile = File.read('Gemfile')
  puts "@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@"
  # find first line that starts with "# " and remove it
  new_gemfile = original_gemfile.sub("# ", '')
  gemfile_diff = original_gemfile.split("\n") - new_gemfile.split("\n")
  if gemfile_diff.size == 0
    puts "No diff"
    exit(0)
  end
  puts "Diff: #{gemfile_diff}"
  File.write('Gemfile', new_gemfile)

  process = nil
  process_output = []

  ::Open3.popen2e(
    'bundle install'
  ) do |_input, stdout_and_stderr, wait_thr|
    process = wait_thr
    io = stdout_and_stderr
    f = IO.select([io])[0][0]
    process_output.push f.readline until f.eof?
  end
  exit_status = process.value.exitstatus.to_i
  puts("Exit status: #{exit_status}")
  if exit_status != 0
    puts "Error: #{process_output.join("\n")}"
    skiped_gemfile = original_gemfile.sub("# ", "#! ")
    File.write('Gemfile', skiped_gemfile)
  end
  sleep 30
end
```