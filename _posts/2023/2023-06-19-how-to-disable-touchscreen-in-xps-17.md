---
title: "How to Disable Touchscreen in Ubuntu 20.04 on a Dell XPS 17"
categories: ["linux", "ubuntu", "xps"]
---

The touchscreen feature on a laptop can sometimes be more of a hindrance than a help. There are times when you might accidentally touch the screen, resulting in unwanted clicks or drags. Thankfully, there's an easy way to disable this feature on your Dell XPS 17 running Ubuntu 20.04.

First, **identify your touchscreen device** by opening the Terminal. You can do this by searching for "Terminal" in your applications menu, or by pressing `Ctrl+Alt+T`. In the terminal, type the following command:

```bash
xinput
```
This command will display a list of all input devices. Find your touchscreen in this list, which might be named something like "ELAN Touchscreen" or "FTSC1000:00 2808:1015".

Next, **disable the touchscreen** using the `xinput disable [id]` command, replacing [id] with your touchscreen device's ID number. If your touchscreen's ID is 10, for instance, you would enter:

```bash
xinput disable 10
```
Please remember to replace [id] with your own device's ID. Be careful not to disable other devices as it might affect the functionality of your mouse, keyboard, or other important input devices.

This method will only disable the touchscreen until the next reboot. For a permanent solution, consider adding the command to a startup script. However, the process to do this may vary depending on your desktop environment.

By following these steps, you can easily control the touchscreen feature on your Dell XPS 17 and make your Ubuntu 20.04 experience even more enjoyable.

---

_Disclaimer:_ Be sure to replace "[id]" with the actual ID number of your touchscreen. Each hardware configuration will have a unique ID. Be careful not to disable any other devices, as you might lose the ability to use your mouse, keyboard, or other important input devices.