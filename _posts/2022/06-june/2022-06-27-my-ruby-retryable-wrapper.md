---
title: "My Ruby Retryable Wrapper"
categories: ["ruby","ruby-on-rails","programming","optimization"]
---

Code snippet:
```ruby
require 'timeout'

module Retryable
  def with_retries(*args)
    options = args.extract_options!
    exceptions = args

    options[:limit] ||= 3
    exceptions = [StandardError] if exceptions.empty?

    retried = 0
    begin
      if options[:timeout_in]
        Timeout.timeout(options[:timeout_in]) do
          yield
        end
      else
        yield
      end
    rescue *exceptions => e
      raise e if retried + 1 >= options[:limit]

      retried += 1
      retry
    end
  end
end
```

Source: 
 * <https://scoutapm.com/blog/ruby-retry>
 * <https://gist.github.com/cainlevy/1323593/2321056de18e63436e66562e218a631d32077a20>