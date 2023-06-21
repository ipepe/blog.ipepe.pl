---
title: "Flat file structure in Paperclip + UFS = Disaster"
categories: ["ruby","ruby-on-rails","file-storage", "paperclip"]
---

Introduction:
Today, while working on my Ruby on Rails application, I encountered an interesting file storage problem. The filesystem returned an "Input/output error" when attempting to upload a user attachment. It's important to note that my attachments are accessible via NFS, with the share hosted on FreeBSD. After searching for information on the "file limit of UFS," I couldn't find any relevant results. Frustrated, I turned to my trusted ##techsupport IRC channel for help. Fortunately, a user named `@PipeItToDevNull` provided a valuable answer, directing me to this link: [link](http://www.tek-tips.com/viewthread.cfm?qid=1484502).

Explanation:
According to the information I found, the maximum number of directories allowed in the Solaris[TM] Operating Environment is determined by the LINK_MAX parameter. This parameter is defined as 32767 in the `/usr/include/limits.h` header file and cannot be changed. Since each directory, even an empty one, already contains 2 links (to itself '.' and to the parent '..'), the total available number of directories goes down to 32765. In general, it would be challenging to exceed the total number of directories on a filesystem unless attempting to create more than 32765 subdirectories within a single directory.

Overcoming the Limit:
Realizing that I had hit this limit, I needed to come up with a new structure for my files. To solve this problem, I sought assistance from a co-worker, and together we devised a new path structure: `/storage/:id_divided_by_1000000/:id_divided_by_1000/:id_modulo_1000/file.extension`. This structure allows me to handle up to 32k*1kk (32 billion) files, which is more than sufficient for this project. It's worth noting that this solution works specifically for integer-based IDs.

Implementation:
To implement this new structure with Paperclip, I added the following code:

```ruby
Paperclip.interpolates :id_divided_by_1000000 do |attachment, style|
  (attachment.instance.id / 1_000_000).to_i
end
```

By utilizing this interpolation, I can divide the ID by 1,000,000 to obtain the first part of the path, divide it by 1,000 to get the second part, and calculate the modulo 1000 to determine the third part. This approach ensures a well-organized file structure while avoiding the limitations imposed by the UFS filesystem.

Migration:
In order to implement this new structure, I will need to migrate the existing files to match the new path format. This step is crucial for seamless integration and efficient management of the file storage system.

Conclusion:
Encountering the file storage limit in my Ruby on Rails application led me to explore alternative approaches to handle attachments efficiently. By combining the power of Paperclip and the new path structure, I can overcome the UFS limitations and ensure the successful management of a large number of attachments.