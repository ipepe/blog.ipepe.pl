---
title: "Guide to Setting Up Native Ruby on M1 Macs"
categories: ["ruby", "mac"]
---

This blog post will guide you through the process of setting up native Ruby on M1 Macs. Follow these steps:

1. **Ensure You're Running a 'Clean' macOS Monterey**: The newer versions of macOS have updated C compilers that can't compile older Ruby runtimes. For this reason, it's necessary to ensure your operating system is a 'clean' macOS Monterey.

2. **Install Rosetta 2**: Rosetta 2 is a translation process that enables M1 Mac applications to run software coded for Intel processors. Install it using the following command:
    ```shell
    softwareupdate --install-rosetta --agree-to-license
    ```

3. **Install Xcode Command Line Tools**: These are a set of utilities that software developers use to build software. You can install it with this command:
    ```shell
    xcode-select --install
    ```

4. **Configure Terminal App to Run in Rosetta**: If you're using iTerm, you'll need to set it up similarly to the Terminal app.
    * Useful sources: [BetterProgramming](https://betterprogramming.pub/5-things-i-have-learned-when-using-the-m1-chip-macbook-air-a77f93c50381#5a64) and [Apple StackExchange](https://apple.stackexchange.com/questions/428768/on-apple-m1-with-rosetta-how-to-open-entire-terminal-iterm-in-x86-64-architec)

5. **Install Homebrew in Rosetta Terminal**: Homebrew is a package manager that simplifies the installation of software on Apple's macOS operating system. Use the following command for installation:
    ```shell
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

6. **Add Export Statements to Your `.bash_profile`**: The following lines need to be added to your `.bash_profile`:
    ```shell
    export RUBY_CFLAGS="-Wno-error=implicit-function-declaration"
    export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES
    ```

7. **Install rbenv with ruby-build Using Basic Git Checkout**: rbenv provides support for specifying application-specific versions of Ruby. The ruby-build plugin adds rbenv install command for compiling and installing different versions of Ruby on UNIX-like systems. You can check the process [here](https://github.com/rbenv/rbenv#basic-git-checkout) and for installing ruby-build, click [here](https://github.com/rbenv/ruby-build#clone-as-rbenv-plugin-using-git).

8. **Install Relevant Ruby Versions in Rosetta Terminal**: Use the following commands to install all necessary Ruby versions:
    ```shell
    rbenv install 2.3.8
    rbenv global 2.3.8
    gem install bundler
    ```

9. **Install `pg` Gem**: The `pg` gem provides an interface to the PostgreSQL RDBMS. To install it, execute these commands:
    ```shell
    brew install libpq
    gem install pg -v '0.18.4'
    ```

Follow this guide carefully to successfully set up native Ruby on your M1 Macs.
