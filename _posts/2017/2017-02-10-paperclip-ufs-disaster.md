---
title: "Paperclip + UFS = Disaster"
categories: ["ruby","ruby-on-rails","file-storage", "paperclip"]
---

Today I stumbled upon very intersting file storage problem in Ruby on Rails application: filesystem told us "Input/output error" when trying to upload attachment by user. Bear in mind that my attachments are availble by nfs wchich share is hosted on FreeBSD. So I googled for "file limit of UFS" and didn't get anything. So I asked on my favorite ##techsupport IRC. And sure enough I got and anwser by `@PipeItToDevNull` (thanks!) who gave me this link:
<http://www.tek-tips.com/viewthread.cfm?qid=1484502>

Quote:
```
The maximum number of directories allowed in the Solaris[TM] Operating
Environment is limited by the LINK_MAX parameter.

This parameter is defined as 32767 in the /usr/include/limits.h
header file and it cannot be changed.

Since each directory (even an empty one) already contains 2 links
(to itself '.', and to the parent '..'), the total available goes
down to 32765.  In general, you would be hard pressed to exceed the
total number of directories you can have on a filesystem unless you are
trying to create more than 32765 sub-dirs. in any single directory.
```


And that is enough for me. I hit the limit, so I had to came up with new structure for files.

But how I got into this situation in the first place? Well, my project
is ruby on rails based and I use paperclip gem to handle attachments.
And today was a day when my users created 32765th attachment in my
application.

To solve this problem I asked my co-worker for help. And with his help
we came up with this path structure:
`/storage/:id_divided_by_1000000/:id_divided_by_1000/:id_modulo_1000/file.extension`

This way I will be able to handle 32k*1kk files which is sufficient for
this project. Of course I have to migrate old files and this will only
work for integer based id's.

```ruby
Paperclip.interpolates :id_divided_by_1000000 do |attachment, style|
  (attachment.instance.id / 1_000_000).to_i
end
```