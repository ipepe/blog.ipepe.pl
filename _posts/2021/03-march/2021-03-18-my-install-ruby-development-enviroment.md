---
title: My Install of Ruby Development Environment
categories: ruby
---

 * Install rbenv (https://github.com/rbenv/rbenv#basic-github-checkout)
   * If You don't have git on Your Mac, You need to run: `xcode-select --install`
   * `git clone https://github.com/rbenv/rbenv.git ~/.rbenv`
   * `cd ~/.rbenv && src/configure && make -C src`
     * this is optional, it compiles bash exstension
   * `mkdir -p ~/.rbenv/plugins`
   * `git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build`
   * Add to ~/.bash_profile
     * `export PATH="$HOME/.rbenv/shims:$HOME/.rbenv/bin:$PATH"`
     * `eval "$(rbenv init -)"`
   * reload terminal window 
   * `rbenv install 2.3.1`
   * `rbenv global 2.3.1`
 * Install nodenv (https://github.com/nodenv/nodenv#basic-github-checkout)
   * `git clone https://github.com/nodenv/nodenv.git ~/.nodenv`
   * `cd ~/.nodenv && src/configure && make -C src`
     * this is optional, it compiles bash exstension
   * `mkdir -p ~/.nodenv/plugins`
   * `git clone https://github.com/nodenv/node-build.git ~/.nodenv/plugins/node-build`
   * Add to ~/.bash_profile
       * `export PATH="$HOME/.nodenv/bin:$HOME/.nodenv/shims:$PATH"`
       * `eval "$(nodenv init -)"`
   * reload terminal window
   * `nodenv install 8.11.3`
   * `nodenv global 8.11.3`
 * Install Postgres desktop App for Mac
   * https://postgresapp.com/
   * Add to ~/.bash_profile
     * `export PATH=$PATH:/Applications/Postgres.app/Contents/Versions/latest/bin`
   * Run SQL queries:
     * In Postgres app double click on "postgres databas"
     * OR run in terminal: `/Applications/Postgres.app/Contents/Versions/13/bin/psql -p5432 "postgres"`
     * `CREATE USER webapp WITH PASSWORD 'webapp';`
     * `ALTER USER webapp WITH SUPERUSER;`
 * `brew install imagemagick`
 * install Docker desktop for Mac
   * https://www.docker.com/products/docker-desktop
   * `docker run -p 6379:6379 --restart=unless-stopped -d --name redis redis:alpine`
 * In project repository
   * `gem install bundler:1.17.1`
     * optionally
   * `rbenv rehash`
   * `bundle install`
   * `rbenv rehash`
   * `rails db:create`
   * `rails db:migrate`
   * `rails db:seed`
   * `rails server`
   * `rails console`
     * ie: User.first
     * ie: User.count
     * ie: User.first.update(email: 'user@example.org')
