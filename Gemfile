# frozen_string_literal: true

source 'https://rubygems.org'

# This is the default theme for new Jekyll sites. You may change this to anything you like.
gem 'minima', '~> 2.5'
# If you want to use GitHub Pages, remove the "gem "jekyll"" above and
# uncomment the line below. To upgrade, run `bundle update github-pages`.

# If you have any plugins, put them here!
group :jekyll_plugins do
  gem 'github-pages'
  gem 'jekyll-feed', '~> 0.12'
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem 'tzinfo', '~> 1.2'
  gem 'tzinfo-data'
end

group :development do
  gem 'rubocop'
  gem 'rubocop-jekyll'
  gem 'rubocop-performance'
end

# Performance-booster for watching directories on Windows
gem 'wdm', '~> 0.1.1', platforms: %i[mingw x64_mingw mswin]
