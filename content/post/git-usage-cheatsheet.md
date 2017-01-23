+++
title = "Git Workflow For Small Teams & Usage Cheatsheet"
draft = false
date = "2016-04-03T19:17:24+08:00"
tags = ["git", "workflow", "cheatsheet"]
categories = ["Software Engineering"]

+++

In a simple context of *Software Development*, I assume there are roles of **Developers**, **Technical Lead** and **Non-developers (Testers)**, and all the set-ups are done.

Note: **origin** refers to the remote repo.

### 1. Source code Update for All

Update the latest remote code from Remote repo to local Git repo:

`$ git fetch`

Merge the latest code from origin/master to local master branch:

`$ git checkout master`

`$ git merge origin/master`

Now the local master is reflected the latest code on office1. If there are reported conflicts, resolve the conflicts, then commit it to local master:

`$ git commit -m “Message to be entered”`

### 2. Feature Implementation/ Bug Fixing for Developer

From branch master, create new branch:

`$ git branch feature01`

Now start working on the feature01. Stage the modifications from time to time:

`$ git add .`

When the set of modifications are stable and the unit testing is fine, commit to local branch (assume on branch feature01):

`$ git commit -m “Commit Message. For example: Commit Beta version v0.1”`

### 3. Push to remote server for Developer

Make sure the code is tested thoroughly and committed to branch feature01. Now merge it back to local master:

`$ git checkout master`

`$ git merge feature01`

If there is no other working branch, the merge should be fast forward and no conflicts. However, there are cases whereby local master was merged with some other branches before. In these cases, resolve conflicts and commit local master.

Next important step, test the feature thoroughly, if there are some small issues, resolve it on local master.

So, after this, local master should be the best and latest working branch on local machine. Now, push local master to the remote branch, assume now on local branch local master.

If this is the first push, and the branch is supposed to be newly created:

`$ git push origin master : developer-name-feature01`

Else, push it to the working remote branch:

`$ git push origin developer-name-feature01`

At this stage, all the work done is now on origin/developer-name-feature01 for review.

Switch back to branch feature01 if there is more work to be made:

`$ git checkout feature01`

Merge branch master to feature01 for latest update.

`$ git merge master`

If there are issues, resolve again before continue working on this branch (feature01).

Otherwise, everything is done with feature01, delete it entirely for local repo cleanliness:

`$ git checkout master`

`$ git branch -d feature01`

### 4. Code review for Project Manager/ Tech Lead

Update code from remote server:

`$ git fetch`

See all the pushed branches:

`$ git branch -a`

Rebase / Checkout the branch developer-name-feature01:

`$ git checkout -b feature01 origin/developer-name-feature01`

Now on local branch feature01. Test the code thoroughly. If everything is fine, merge with local master:

`$ git checkout master`

`$ git merge feature01`

If there are conflicts, resolve and commit to local master:

`$ git commit -m “Message to be entered”`

Push the latest code to origin/master:

`$ git push origin master`

Now the new code is ready for everybody. Remove the local branch feature01 for cleanliness:

`$ git branch -d feature01`

### 5. Miscellaneous commands:

Delete a redundant remote branch:

`$ git push origin : feature01`

Sometimes, a local working branch is longer used, but cannot be deleted since there is some uncommitted modifications. Force delete:

`$ git branch -D feature01`

Stage deleted files before commit:

`$ git add -u`

Fetch the remote repo with all the deleted branches

`$ git fetch -p`

Clear the untracked folders from being tracked to staging area

`$ git clean -f -d`

To update the remote branch list:

`$ git remote update`

To change username:

`$ git config --global user.name "Captain America"`

To change email:

`$ git config --global user.email "batman@superman.ironman"`

### 6. Important Notes:

**For Developers:**

The local branch master should always be the cleanest back up.
When update the source code to local repo, developer should always fetch and merge with origin/master, not any other branches.

When push work to remote, developer should always merge the work with local master, and only push from local master to his own branch on remote. Never push directly to origin/master. Only Reviewer (Project Manager, Tech Lead) can push directly to origin/master for the sake of cleanliness.

**For Reviewers:**

Always checkout new branch when reviewing developer’s code.
Always merge the local branch to local master before pushing to remote. When pushing to remote, only push to origin/master.

**For Everyone:**

Regularly update the **origin/master** with **local master** for synchronization with everyone’s work.
Make sure git pull is understood when using. Git fetch + git merge produce the same work, but in a safer way.

Stage code regularly. Don't lose your work.