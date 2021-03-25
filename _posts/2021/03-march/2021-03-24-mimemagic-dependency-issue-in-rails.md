---
title: MIMEMAGIC dependency issue in rails
categories: ruby
---

Hey. I don't know if You have already seen: <https://github.com/rails/rails/issues/41750> but it causes failed builds. 

As a quick fix, add this to Gemfile:
```ruby
gem "mimemagic", git: "https://github.com/minad/mimemagic.git", ref: "d5ebc0cd846dcc68142622c76ad71d021768b7c2"
```
Or (but I can't promise it will be there forever)
```ruby
gem "mimemagic", git: "https://github.com/ipepe-oss/mimemagic.git"
```
