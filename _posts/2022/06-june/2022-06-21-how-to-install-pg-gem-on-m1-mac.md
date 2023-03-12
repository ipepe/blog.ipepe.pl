---
title: "How to install pg on M1 Mac"
categories: ["postgres", "ruby", "devops", "programming"]
---

If You have problem installing pg gem on M1 Mac, or other native extension You can try this:
 * `brew install libpq`
   * helps with `nio4r` install
 * `gem install pg -v '0.18.4' -- --with-cflags="-Wno-error=implicit-function-declaration"`
 *  brew install v8-315
   * gem install therubyracer -v '0.12.2' -- --with-v8-dir=/usr/local/opt/v8@3.15

If You have multiple projects then I recommend configuring this in global bundler config: 
```bash
bundle config set --global build.pg --with-cflags=-Wno-error=implicit-function-declaration
```

Or you can add this config to `.bash_profile`:
`export RUBY_CFLAGS="-Wno-error=implicit-function-declaration"`

