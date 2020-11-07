---
tags: ruby rails rspec testing
---
# You should lint Your factories

In RSpec I often encounter projects where Factories are not being linted. This is important, because tests may pass, but once You start writing new functionality it may occur that factory is invalid. Quick snipped for all of You that want to start linting:

```ruby
# spec/models/factory_girl_spec.rb

require 'rails_helper'

describe FactoryGirl do
  described_class.factories.each do |factory|
    describe "#{factory.name} factory" do
      it 'is valid' do
        described_class.lint [factory], traits: true
      end
    end
  end
end
```