---
title: "M1 MacBook with native Ruby"
categories: ["ruby", "macos", "devops", "programming"]
---


1. Ensure you are running "clean" macOS Monterey (newer macOS has newer C compiler that fails when compiling older Ruby runtimes).
2. Install Rosetta 2
   * `softwareupdate --install-rosetta --agree-to-license`
3. Install Xcode Command Line Tools
    * `xcode-select --install`
4. Setup Terminal app to run in Rosetta (if you use iTerm, setup it similiarly)
  * Sources: <https://betterprogramming.pub/5-things-i-have-learned-when-using-the-m1-chip-macbook-air-a77f93c50381#5a64> and <https://apple.stackexchange.com/questions/428768/on-apple-m1-with-rosetta-how-to-open-entire-terminal-iterm-in-x86-64-architec>
6. Install Homebrew (in Rosetta Terminal)
   * `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"` 
5. Add to your `.bash_profile`:
    * `export RUBY_CFLAGS="-Wno-error=implicit-function-declaration"`
    * `export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES`
6. Install rbenv (with ruby-build) using Basic Git Checkout
    * Source: <https://github.com/rbenv/rbenv#basic-git-checkout>
    * Install ruby-build: <https://github.com/rbenv/ruby-build#clone-as-rbenv-plugin-using-git>
6. Install all relevant Ruby versions (in Rosetta Terminal)
   * `rbenv install 2.3.8`
   * `rbenv global 2.3.8`
   * `gem install bundler`
7. Install Postgres db with <https://postgresapp.com/>
8. Start redis using Docker: `docker run -p 6379:6379 --restart=unless-stopped -d --name redis redis:alpine`
10. Setup pg config and install `pg` gem
   * (Optionally only if gem install pg doesn't work) `brew install libpq`
   * `bundle config build.pg --with-pg-config=/Applications/Postgres.app/Contents/Versions/latest/bin/pg_config`
   * `gem install pg`
11. Setup libv8 and rubyracer, and install `therubyracer` gem
   * Source: <https://gist.github.com/fernandoaleman/868b64cd60ab2d51ab24e7bf384da1ca?permalink_comment_id=4112276>
   * `bundle config build.libv8 --with-system-v8`
   * `bundle config build.therubyracer --with-v8-dir=$(brew --prefix v8@3.15)`
   * `gem install therubyracer`
12. Setup and install for nokogiri
   * `brew install libxml2`
   * `bundle config build.nokogiri --use-system-libraries --with-xml2-include=$(brew --prefix libxml2)/include/libxml2`
   * `gem install nokogiri`
