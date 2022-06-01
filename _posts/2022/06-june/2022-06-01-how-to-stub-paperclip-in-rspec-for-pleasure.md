---
title: "How to stub Paperclip in RSpec for Pleasure"
date: "2020-06-01"
categories: ["Rails", "RSpec"]
---

I have a lot of models with images in one of my Rails applications. And recently I optimized my tests execution time by simply stubbing Paperclip:
```ruby
module Paperclip
  class Attachment
    def post_process; end
  end
  def self.run(cmd, arguments = '', interpolation_values = {}, local_options = {})
    cmd == 'convert' ? nil : super
  end
end
```

But I didn't like that approach because it limited my whole test suit to never use paperclip. Today I needed to write full integration test that used whole codebase including paperclip and convert feature. I sat down and came up with this:

```ruby
RSpec.configure do |config|
  config.before(:each) do |example|
    unless example.metadata[:with].try(:include?, :original_paperclip)
      allow_any_instance_of(Paperclip::Attachment).to receive(:post_process)
      allow(Paperclip).to receive(:run).and_call_original
      allow(Paperclip).to receive(:run).with("convert").and_return(nil)
    end
  end
end
```

This allows for paperclip stub to be turned off per test example basis by writing:

```ruby
it "does something", with: [:original_paperclip] do
  # your test code here
end
```

The way this is written, it allows for many different stubbing scenarios to be turned off or on in simple syntax for each example.