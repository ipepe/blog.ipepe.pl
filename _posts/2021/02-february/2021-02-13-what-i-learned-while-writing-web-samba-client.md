---
title: What I learned while writing web Samba client
categories: samba
---

I recently started working on project for a web based client of samba share. I want to use it for Chromecast streaming of 


## Rails ActionController::Live
You can stream content with http using ActionController::Live this is very interesting piece of tech that allows You to deliver content as You generate it. It is especially useful when content might be long. 
```
class MessagesController < ApplicationController
  include ActionController::Live

  def index
    @messages = Message.all
  end

  def create
    @message = Message.create!(params[:message].permit(:content, :name))
  end

  def events
    3.times do |n|
      response.stream.write "#{n}...\n\n"
      sleep 2
    end
  ensure
    response.stream.close
  end
end
```

## /dev/fd/1 is used as file/io pipe
This is very good example of using `/dev/fd`. `/dev/fd/1` is specially crafted file that corresponds to STDOUT of process that is accesing it. 
`smbclient -E -U $USERNAME //server/sharename $PASSWORD -c 'get \\dir\\filename.gz /dev/fd/1' 2>/dev/null | zcat | yourcommand`

## curl can be used to download files from Samba shares (only v1)
curl supports the smb protocol since v7.40 (<https://www.phoronix.com/scan.php?page=news_item&px=MTg4MzI>):
 * `curl --upload-file /path/to/file.ext  -u 'DOMAIN\Username' smb://172.16.17.52/ShareName/`
 * `curl --upload-file /home/me/moderately_sized_file --user "OurWindowsDomain/MyUserName:MyPassword" smb://172.16.17.52/OurRemoteDirectory/Path/To/Dir/`

Sources:
 * <https://piotrmurach.com/articles/streaming-large-zip-files-in-rails/>
 * <http://railscasts.com/episodes/401-actioncontroller-live?view=asciicast>
 * <https://unix.stackexchange.com/questions/190391/using-smb-to-pipe-contents-of-file-to-local-command-on-local-machine>
 * <https://unix.stackexchange.com/questions/206415/sending-files-over-samba-with-command-line>
