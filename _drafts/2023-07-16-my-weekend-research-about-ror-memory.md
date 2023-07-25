---
title: "My weekend research about Ruby on Rails memory usage"
categories: ["ruby", "rails"]
---

I recently wrote a very small Ruby on Rails application that will probably stay small for rest of its life, but I'm planning on hosting it for quite some time. I wanted to know how small VPS I can take to host it. I did some research and here are my findings.

## Ruby on Rails memory usage

I was wondering what is typical RoR application memory usage. I know applications where single Ruby process can start at around 400MB and after use it can grow into over 1GB and probably more. But I had trouble to establish what is lowest memory usage that I can expect from RoR application. From <https://discuss.rubyonrails.org/t/256mb-of-ram-enough-for-ruby-on-rails-and-mysql/20499> we can see user reporting that they manage to host Rails with MySLQ on 256MB VPS which is impressive, but that is at 2007 and Rails was at first major version and second major release was about to be published in few months. I'm sure Rails did change a lot since then, but lower memory consumption was not a goal of those changes.


## Testing methodology

I created Rails using `rails _X.Y.Z_ new` in Ruby 2.7 