---
title: "How to install pg on M1 Mac"
categories: ["postgres", "ruby", "devops", "programming"]
---

If You have problem installing pg gem on M1 Mac, or other native extension You can try this:
 * `brew install libpq`
   * helps with `nio4r` install
 * `gem install pg -v '0.18.4' -- --with-cflags="-Wno-error=implicit-function-declaration"`



