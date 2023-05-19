---
title: "Why small 'it's are bad"
categories: ["ruby", "rails", "testing"]
---

I recently was tasked with optimizing a very slow test suite. While looking at it, I noticed that we had a lot of small `it` blocks that had very slow `before` blocks running before them. 

Instead of running each `it` block separately with the entire setup each time, a clever solution was provided by [TestProf](https://test-prof.evilmartians.io/) through their `RuboCop` cops. They encourage using one of RSpec's excellent features – the aggregation of failures within a single example. This approach permits grouping independent assertions together, running all setup hooks only once and considerably boosting test suite performance by reducing the total number of examples. 

This change required only a minor alteration to our `.rubocop.yml` file to enable the `RuboCop` cops:

```yml
# .rubocop.yml
require:
 - 'test_prof/rubocop'
```

One of the cops provided by TestProf is `RSpec/AggregateExamples`. Here's an example of how to modify your tests to take advantage of it:

```ruby
# before
it { is_expected.to be_success }
it { is_expected.to have_header("X-TOTAL-PAGES", 10) }
it { is_expected.to have_header("X-NEXT-PAGE", 2) }
its(:status) { is_expected.to eq(200) }

# after
it "returns the second page", :aggregate_failures do
  is_expected.to be_success
  is_expected.to have_header("X-TOTAL-PAGES", 10)
  is_expected.to have_header("X-NEXT-PAGE", 2)
  expect(subject.status).to eq(200)
end
```

Notice that we now have just a single `it` block with multiple assertions. This allows the setup (the `before` blocks) to run only once for this group of assertions, rather than once per assertion, dramatically speeding up our test suite.

Also, TestProf's `RuboCop` cops come with an auto-correct feature, which can make these adjustments automatically!

For more details on this and other cops provided by TestProf, you can check out their [documentation](https://test-prof.evilmartians.io/#/misc/rubocop?id=rspecaggregateexamples). Happy testing!

Sources:
 * <https://test-prof.evilmartians.io/#/misc/rubocop?id=rspecaggregateexamples>