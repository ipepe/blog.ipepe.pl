---
title: "Boost Your Efficiency as a Developer with These 3 Mac OS Hacks"
categories: ["macos", "devops"]
---

Introduction:
Being a developer on Mac OS can be enhanced by leveraging scripts, commands, and settings that optimize your workflow and boost your productivity. In this blog post, we will explore three valuable Mac OS hacks that can significantly improve your efficiency as a developer.

## 1. Creating New Text Files in Finder
One feature that many developers miss from Windows is the ability to quickly create a new text file while browsing through directories. Fortunately, you can replicate this functionality in Mac OS with a simple workflow in Finder.

```applescript
tell application "Finder"
    set txt to make new file at (the target of the front window) as alias with properties {name:"New Text File.txt"}
    select txt
end tell
```

With this workflow, you can effortlessly create new text files in Finder, streamlining your file management process.

## 2. OCR Text from Images
As developers, we often come across situations where we need to extract text from images, such as code snippets in tutorials or documentation. Mac OS provides a built-in OCR (Optical Character Recognition) capability that eliminates the need for additional tools or libraries. By creating a shortcut, you can easily extract text from an image.

Follow these steps to set up the shortcut using the Shortcuts app on your Mac:

1. Open the Shortcuts app on your Mac.
2. Create a new shortcut.
3. Build the following workflow:

```shortcut
Receive Any input from QUICK Actions
If there's no input:
Continue
Take Interactive screenshot
Extract text from Screenshot
Combine Text from Image with New Lines
Copy Combined Text to clipboard
```

This shortcut empowers you to effortlessly copy text from images, enhancing your ability to extract valuable information from various sources.

## 3. Accelerate Your Terminal with Key Repeat
Waiting for terminal commands to catch up can be frustrating and time-consuming. By adjusting the key repeat settings, you can significantly speed up your terminal navigation, particularly when using arrow keys and the backspace key.

**Note: You need to restart your Mac after executing these commands.**

To modify the key repeat settings, follow these steps:

1. Open the Terminal app.
2. Execute the following commands:

```bash
defaults write -g KeyRepeat -int 1
defaults write NSGlobalDomain KeyRepeat -int 1
```

3. Restart your Mac.

By implementing these settings, you will experience a noticeable improvement in your terminal navigation speed.

## Sources:
* [Gist: Mac OS Automator](https://gist.github.com/lachok/5b401268c82b7f4b4a55)
* Mac OS Shortcuts
* [YouTube: Extract text from images with Mac OS](https://www.youtube.com/watch?v=BZVlifUpr_c)

Conclusion:
By utilizing these three Mac OS hacks, you can streamline your development workflow, enhance your productivity, and save valuable time. Creating new text files in Finder, extracting text from images, and optimizing your terminal navigation are just a few examples of how you can boost your efficiency as a developer on Mac OS. Incorporate these hacks into your routine and enjoy a smoother and more productive development experience.