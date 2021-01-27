---
title: Why sequencing migrations in Rails is bad idea?
categories: programming
---

Recently I wrote quite big and extensive database migration in Rails. (ie. `1000_restructure_users.rb`) In code review I have got a suggestion to split it into parts. And so I did:
 * `999_add_new_columns.rb`
 * `1000_migrate_data_in_users.rb`
 * `1001_remove_old_columns.rb`

I did a mistake and I simply created two files with +1 and -1 numbers in migration timestamp. It bit me hard when third migration failed and I couldnt write a migration between second and third migration because atomic increase was impossible and there was no space to add it.

So if You are copying or spliting database migrations into parts, leave Yourself some space for some unexpectedly coming fixes. 