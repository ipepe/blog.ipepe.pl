---
titile: My fresh MacBook install
categories: programming
---

* Chrome
    * https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc/related
    * adblock
    * https everywhere
* Rubymine
    * uncheck show tabs in one row
*  Docker
    * Docker login in cli
    * add /opt/docker to shared directories
    * `docker run -p 6379:6379 --restart=unless-stopped -d --name redis redis:alpine`
* Postgres app
    * pg_config env
    * export PATH=$PATH:/Applications/Postgres.app/Contents/Versions/latest/bin
    * run queries:
        * `CREATE USER webapp WITH PASSWORD 'webapp';` 
        * `ALTER USER webapp WITH SUPERUSER;` 
* Key Repeat
    * defaults write -g KeyRepeat -int 1
    * defaults write NSGlobalDomain KeyRepeat -int 1
* Don’t create DS_Store on network shares
    * defaults write com.apple.desktopservices DSDontWriteNetworkStores true
* Install brew
    * `brew install imagemagick`
* Global Gitignore
    * See my other post: Global gitignore
    * git config --global core.excludesfile ~/.gitignore
    
* http://docs.hardentheworld.org/OS/OSX_10.11_El_Capitan/#require-password-to-un-lock
* https://github.com/barnybug-archive/docker-fish-completion
    * https://github.com/fisherman/fisherman
* Git config global user name user email
    * `git config --global user.name "John Doe"`
    * `git config --global user.email johndoe@example.com`
    * `git config --global push.default current`
* install fish
    * fish >> .bash_profile
    * prompt: informative vcs
    * docker auto-complete
        * wget https://raw.github.com/barnybug/docker-fish-completion/master/docker.fish -O ~/.config/fish/completions/docker.fish
* TextMate
    * ln -s /Applications/TextMate.app/Contents/Resources/mate /usr/local/bin/mate
* Macs Fan Control
* ZeroTier-One
* Microsoft Remote Desktop
* VirtualBox
* Etcher.io
* Finder
    * Empty trash after 30 days
* Disk Inventory X
* VLC
    * Qnapi
* ngrok
* ssh configs and keys
* https://tclementdev.com/timemachineeditor/

