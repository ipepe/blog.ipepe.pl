---
title: Transfering GIT repository between machines
categories: programming
---

Sometimes when working in very unique teams and scenarios, You need to transfer git changes between machines without using common server.

## GIT Bundle

GIT bundle should be a way to go for every programmer when You need to transfer git repository. Using GIT bundle guarantees that commit history is kept.
 
Commands:
 * Create bundle: `git bundle create git_repo.bundle main`
 * Clone from bundle: `git clone -b master git_repo.bundle project_name`
 * Add bundle as additional origin: `git remote add bundle file.bundle; git pull bundle main`

## GIT Patch
Sometimes You need to send a quick patch, this is useful when You already have a repository with changes and You only need transfer some small changes or additions. It's a simple 2 steps process:
 * Generate the patch: `git diff > some-changes.patch`
 * Apply the diff: `git apply some-changes.patch`

## GIT Archive

Sometimes You might want to share Your repository contents without history. This might be for multiple reasons: 
 * Code deployment to server
 * Sharing code with end users
 * Repository history is too big/to long

Commands:
 * Create zip archive: `git archive -o latest.zip HEAD`
 * Create zip archive: `git archive -o latest.zip HEAD`


 