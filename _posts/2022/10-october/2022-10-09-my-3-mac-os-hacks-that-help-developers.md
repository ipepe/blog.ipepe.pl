---
title: "My 3 Mac OS hacks that help developers"
categories: ["macos", "devops"]
---

To work efficently on Mac OS, there are some scripts/commands and settings you can tune to work faster.

## 1. Create new text file in Finder
I really miss this option from Windows, it happens often that I'm in some directory and I need to create quickly a new txt file. With this workflow you can easily do that in Finder.


```workflow
tell application "Finder"
	set txt to make new file at (the target of the front window) as alias with properties {name:"New Text File.txt"}
	select txt
end tell
```

## 2. OCR text from image
Often I find myself in a situation where I need to copy some text from an image, youtube video (coding tutorials) or any other place where you cannot easily copy text. With this Shortcut you can easily copy text from an image using Mac OS built in OCR. No need to install additional tools or libraries.

1. Open Shortcuts app on your Mac. 
2. Create new shortcut.
3. Create this flow:

```shortcut
Receive Any input from QUICK Actions
If there's no input:
Continue
Take Interactive screenshot
Extract text from Screenshot
Combine Text from Image with New Lines
Copy Combined Text to clipboard
```

## 3. Faster terminal - key repeat

I very impetient with functionalities that take too long, when they don't have to. Especially pressing right/left arrows in terminal or backspace. With this setting you can make it much faster.

*Warning! Restart is required after executing them.*

Open Terminal app and execute these commands:
```bash
defaults write -g KeyRepeat -int 1
defaults write NSGlobalDomain KeyRepeat -int 1
```

And restart your Mac now.

## Sources:
 * <https://gist.github.com/lachok/5b401268c82b7f4b4a55>
 * Mac OS Automator
 * Mac OS Shortcuts
 * <https://www.youtube.com/watch?v=BZVlifUpr_c>