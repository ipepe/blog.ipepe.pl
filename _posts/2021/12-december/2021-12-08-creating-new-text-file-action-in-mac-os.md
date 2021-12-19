---
title: Creating new text file action in Mac OS
date: 2021-12-08
categories: ["macos"]
---

I really miss option of creating new text file in Mac OS in simple way like Windows offers on right click.

To bring it back, we will use Automator.

1. Create Quick Action
2. Change "any window" to "Finder"
3. Change receives to "no input"
4. Add "Run AppleScript" from library
5. Paste the following script:

```applescript
tell application "Finder"
    set txt to make new file at (the target of the front window) as alias with properties {name:"empty.txt"}
    select txt
end tell
```
6. Save it as "New Text File" and close automator
7. "New Text File" will be avaiable in Services menu when Finder is open

Sources:
 * [Create a New Text File Anywhere With a Keyboard Shortcut On a Mac](https://www.youtube.com/watch?v=vAxfNDRz2IY)
 * [How to Quickly Create a New, Blank Text File on Windows, Mac, and Linux](https://www.groovypost.com/howto/quickly-create-new-blank-text-file-windows-mac-linux/)