---
title: You should have multiple language versions
categories: programming
---


When You start programming, You usuallly set up newest version of Your programming language of choice. And that is good, but only in the beginning. Once You start working on multiple projects, You will notcie that they might depend on different version of Your language. At first You might try to update all projects to same version, but it's a good idea only in the beginning. Some times You might want to run only one time a code that was written for different version of Your programming language and You don't want to update it to newest one. Or You might want to check out newest features but without reinstalling language each time You want a different version.

That is why developers came up with "envriomental" versions.

For node it would be `nodenv` or `nvm`

For ruby it would be `rbenv` or `rvm`

For some of You that might be reading this, it is obvious. But some times even experienced programmers do a mistake here. For example You have `rbenv` installed but You don't have `nodenv` installed. Why? You should have node installed also through `nodenv` because as often as You change ruby, node also changes on per project basis.