---
title: "Tools for auditing Rails applications"
categories: ["ruby","ruby-on-rails","programming","audit"]
---

1. "Code reviewer"
   1. [Pronto](https://github.com/prontolabs/pronto)
2. Static code analysis (lint/style)
   1. [Rubocop](https://docs.rubocop.org/rubocop/installation.html)
   2. [MetricFu - includes most others](https://github.com/metricfu/metric_fu)
   3. [Reek](https://github.com/troessner/reek)
   4. [Flay - code similiarities](https://github.com/seattlerb/flay)
   5. [RailsBestPractices](https://github.com/flyerhzm/rails_best_practices)
   6. [Fasterer](https://github.com/DamirSvrtan/fasterer)
   7. [Debride](https://github.com/seattlerb/debride)
   8. [RubyCritic](https://github.com/whitesmith/rubycritic)
   9. <https://github.com/CoralineAda/fukuzatsu>
   10. <https://github.com/amatsuda/traceroute> - Find unused routes/controller actions
   11. <https://github.com/seattlerb/flog>
   12. grep
       1. `grep -ir "todo" app`
       2. `grep -ir "has_and_belongs_to_many" app`
   14. Template analysis/lint:
       1. erblint - Lints ERB or HTML files.
       2. haml-lint - Keeps HAML files clean and readable.
       3. markdownlint - Lints Markdown files.
       4. puppet-lint - Checks Puppet manifests conformity with the style guide.
       5. scss-lint - Lints SCSS files.
       6. slim-lint - Lints Slim templates.
       7. yard-junk - Lints YARD documentation.
3. Static code analysis for security
   1. [Brakeman](https://brakemanscanner.org/docs/quickstart/#reporting)
   2. <https://github.com/thesp0nge/dawnscanner>
4. Gemfile analysis
   1. Bundler audit
   2. <https://github.com/rubymem/bundler-leak> - memory leak checking
   3. https://github.com/appfolio/gemsurance
   4. Check if gems are hosted on forks that can be pulled from under your own control.
   5. pry-rails on production is no-no
5. Upgrading rails
   1. <https://github.com/clio/ten_years_rails>
   2. <https://github.com/fastruby/next_rails>
6. n+1 detection
   1. Bullet gem + tests
7. Code coverage
   1. SimpleCov + tests
   2. Production: <https://github.com/danmayer/coverband>
   3. Keep Your code coverage feedback loop short: <https://github.com/grodowski/undercover>
8. Ruby version analysis
   1. https://github.com/civisanalytics/ruby_audit
9. ORM+schema consistency check
   1. <https://github.com/gregnavis/active_record_doctor>
   2. <https://github.com/trptcolin/consistency_fail>
   3. <https://github.com/plentz/lol_dba>
   4. <https://github.com/matthuhiggins/foreigner>
   5. <https://github.com/KevinColemanInc/yeet_dba>
   6. <https://github.com/djezzzl/database_consistency>
   7. <https://github.com/jenseng/immigrant>
   8. <https://github.com/ankane/strong_migrations>
10. Licensing check:
    1. license_finder - avoid GPL gems
