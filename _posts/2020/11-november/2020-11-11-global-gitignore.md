---
title: How to setup global gitignore
categories: programming
author: Tony Pujals (github.com/subfuzion)
---

Introduction:

When working with version control systems like Git, it's important to exclude certain files that don't belong in a repository, such as editor-specific files, IDE configurations, or system-generated artifacts. While it's discouraged to clutter the repository's `.gitignore` file with system-specific entries, there is a better approach: using a global gitignore file. In this blog post, we'll explore how to set up and leverage a global gitignore file for improved version control efficiency.

Setting Up a Global Gitignore File:

To start, create a file called `.gitignore` in your home directory and add any files or directories you want Git to ignore. Next, you need to inform Git about your global gitignore file's location. The process differs slightly depending on your operating system.

#### Mac:

Open your terminal and run the following command:

```
git config --global core.excludesfile ~/.gitignore
```

This command updates your `.gitconfig` file to include the following entry:

```
[core]
    excludesfile = {path-to-home-dir}/.gitignore
```

#### Windows:

Open your command prompt or Git Bash and execute the following command:

```
git config --global core.excludesfile %USERPROFILE%\.gitignore
```

This command adds the following entry to your `.gitconfig` file:

```
[core]
    excludesfile = {path-to-home-dir}/.gitignore
```

Customizing Your Global .gitignore:

The contents of your global gitignore file should reflect files and directories that you want to exclude from version control. Here's an example that covers common scenarios:

```
# Node
npm-debug.log

# macOS
.DS_Store

# Windows
Thumbs.db

# JetBrains IDEs
.idea/

# Vim
*~

# General
log/
*.log

# And more...
```

Remember to review the files that don't belong in your local repository by running `git status` before adding them. If any files should be globally ignored, add them to your global gitignore file accordingly.

Integrating with WebStorm:

If you use WebStorm as your IDE, you'll also need to copy the contents of your global gitignore file to its Ignored Files dialog. Here's how you can access it:

#### Mac:

Go to WebStorm > Preferences > Version Control > Ignored Files.

#### Windows:

Navigate to File > Settings > Version Control > Ignored Files.

Alternatives:

Alternatively, instead of creating a `.gitignore` file in your home directory, you can edit the `~/.config/git/ignore` file directly. This approach can provide the same outcome.

Conclusion:

By utilizing a global gitignore file, you can keep your repository's `.gitignore` clean and focused while ensuring that system-specific and generated files are excluded from version control. This approach promotes efficient collaboration and helps maintain a tidy version-controlled project.

Sources:
- [Tony Pujals' Gist](https://gist.github.com/subfuzion/db7f57fff2fb6998a16c)
- [Stack Overflow Answer](https://stackoverflow.com/a/22885996)