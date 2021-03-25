---
title: Open source Rails applications where You can read code
categories: rails
---

## https://github.com/tootsuite/mastodon
This one is really big one. There are a lot of dependecies 

## https://github.com/discourse/discourse

## https://github.com/redmine/redmine

## https://github.com/covoiturage-libre/covoiturage-libre
It's not a good example, there are few techniques that should be marked here as bad:
* putting static data in controllers (use activehash instead)
* don't use activerecord callbacks (use service objects instead)
