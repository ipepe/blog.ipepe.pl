---
title: Setup multiple git and ssh identities
categories: programming
---

## Setup multiple git ssh identities
* Generate your SSH keys as per your git provider documentation.
* Add each public SSH keys to your git providers acounts.
* In your `~/.ssh/config`, set each ssh key for each repository as in this exemple:

  ``` bash
	Host github.com
		HostName github.com
		User git
		IdentityFile ~/.ssh/github_private_key
		IdentitiesOnly=yes
	Host gitlab.com
		Hostname gitlab.com
		User git
		IdentityFile ~/.ssh/gitlab_private_key
		IdentitiesOnly=yes
  ```

## Setup dynamic git user email & name depending on folder

> /!\ Be very carrefull in your setup : **any misconfiguration make all the git config to fail silently !**
Go trought this guide step by step and it should be fine :wink:

The idea here is to use a different git user name & email depending on the folder you are in.

* In your `~/.gitconfig`, **remove** the `[user]` block and add the following (adapt this exemple to your needs) :

  ``` bash
	[includeIf "gitdir:~/code/personal/"]
		path = .gitconfig-personal
	[includeIf "gitdir:~/code/professional/"]
		path = .gitconfig-professional
  ```
* In your `~/.gitconfig-personal`, add your personnal user informations:

  ``` bash
	[user]
		email = user.personal@users.noreply.github.com     # note we use the noreply github mail
		name = personal_username
  ```
* In your `~/.gitconfig-professional`, add your professional user informations:

  ``` bash
	[user]
		email = user.professional@dns.com
		name = professional_username
  ```