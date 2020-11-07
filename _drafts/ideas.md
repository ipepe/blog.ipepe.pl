# Pendriveapps.com
While working on my VHS Digitizing project I also started my CD/DVD digitizing project. I remebered that minimalistic software for ISO images. After quick google I found Pendriveapps.com and oh boy did memories come. That website didn't change much but it still is a vault of goodies.

The app I was looking for is called LCISOCreator. Unfortunately it seems like it doesn't work on Windows 10.

# Ruby cast to boolean:
```ruby
self.job_board_ready = ActiveModel::Type::Boolean.new.cast(job_board_ready)
```

# Rubocop only changed files

```
git diff-tree -r --no-commit-id --name-only HEAD master | xargs ls -d 2>/dev/null | xargs bundle exec rubocop --force-exclusion -a
```