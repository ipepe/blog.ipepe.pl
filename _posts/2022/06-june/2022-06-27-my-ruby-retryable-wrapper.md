---
title: "Enhancing Your Ruby Code: A Retryable Wrapper"
categories: ["ruby","ruby-on-rails","programming","optimization"]
---

As we know, Ruby is a **powerful** and **versatile** language with a multitude of useful features that can simplify our coding life. Among these many aspects, one particularly invaluable feature is the ability to retry a block of code when an exception occurs. Today, I'll be sharing with you my version of a Ruby Retryable Wrapper, designed to manage such retry operations seamlessly and efficiently.

Before we delve into the code, let's discuss the need for such a wrapper. When programming, we often encounter situations where an operation might fail due to exceptions or unexpected conditions. However, many of these failures are not critical and may pass upon a second or third attempt. This is where the *Retryable Wrapper* comes in, as it can automatically retry these operations a certain number of times before finally raising an exception if they still fail.

Let's take a look at the implementation now:

```ruby
require 'timeout'

module Retryable
  def with_retries(*args)
    options = args.extract_options!
    exceptions = args

    # Default retry limit is set to 3 unless specified otherwise
    options[:limit] ||= 3

    # Default exception class to catch and retry is StandardError unless specified otherwise
    exceptions = [StandardError] if exceptions.empty?

    retried = 0
    begin
      # If a timeout is specified, the block of code is executed within that time limit
      if options[:timeout_in]
        Timeout.timeout(options[:timeout_in]) do
          yield
        end
      else
        # Executes the block of code without any timeout limit
        yield
      end
    rescue *exceptions => e
      # If the number of retries exceeds the limit, the exception is raised
      raise e if retried + 1 >= options[:limit]

      # If the number of retries has not reached the limit, increment the retry count and retry the block of code
      retried += 1
      retry
    end
  end
end
```

This module is designed to be mixed into any Ruby class, giving it the ability to retry a block of code a predetermined number of times. It first extracts the options and exceptions from the given arguments, setting defaults if they are not provided. The `with_retries` method then starts a loop, wrapping the given block of code in a timeout if specified. It catches any exceptions, incrementing the retry counter each time. If the limit of retries is reached, it will raise the last caught exception. If not, it retries the block.

This retryable pattern is handy in real-world applications, like dealing with network requests or file operations where failures are common but often temporary.

I encourage you to use this module in your Ruby projects to improve their resilience and error-handling capabilities. It offers an elegant and clean solution to a common problem in programming.

Sources:
* [Scout APM - Ruby Retry](https://scoutapm.com/blog/ruby-retry)
* [CainLevy's Gist](https://gist.github.com/cainlevy/1323593/2321056de18e63436e66562e218a631d32077a20)