# This course learnt from:
# Amigoscode - Git and GitHub Tutorial For Beginners | Full Course [2021] [NEW]
# https://www.youtube.com/watch?v=3fUbBnN_H2c&t=2753s

# I don't care to "install" GIT right now,  because it comes sorta prepackagaged eith my VISUAL-STUDIO 2019: I just add the following directory to my path:
# C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\IDE\CommonExtensions\Microsoft\TeamFoundation\Team Explorer\Git\cmd

GIT SETUP - 00:15:15
====================

# My initial GIT config commands.
git config --global user.name "CobaltSoixante"
git config --global user.email "weingartena@gmail.com"
git config --global color.ui auto

git config -l	#	List all my configuration parameters.

# Ctrl+L = clear screen
# In GIT a REPOSITORY is simply a COLLECTION of various different VERSIONS of a PROJECT.

GIT INIT - 17:40
================

# Verbs is following table are given more-or-less in the order they were mentioned during the lesson:
#
#	WORKSPACE			STAGING-AREA			LOCAL-REPOSITORY		REMOTE-REPOSITORY
#									log
#									show	
#                                       		-commit->
#			-add-> 
#					rm
#			<-diff->
#			<-restore-
#									amend
#	branch
#                                                                                               branch -r (from local console: cur branch on remote repo)
#                                                                                               branch -a (all current branches: LOACAL and REMOTE)
#												-push-> (from LOCAL console)
#       *                                                               *                       <-pull- (from LOCAL console)
#
git init .	# Create new git repository at current directory. RARELY ISSUED: only for new projects.

GIT ADD - 00:22:10
==================

git status	# Shows current git branch and other stuff about the branch.
#
git add index.html	# Added index.html to the staging area.
git rm --cached index.html	# Remove index.html from the staging area. DOES NOT remove the physical file  :-)  .
#
git add .	# Add all files in staging area AND downwards...
git rm -r --cached .	#  Remove all files in staging area and downwards (the -r does the downwards/recursively bit).
git add -A	# Will add your ENTIRE workspace to your stage directory - Up AND Down - even if you are inside a sub-directory (eg ./test).

COMMITS - 00:29:42
==================

git commit -m "bootstrap project"	# Commit [locally] all mofified files in the staging area.
git log					# gives a terse commit history, including commit HASH, MESSAGE, DATE-TIME STAMP.
git show 38b3070a450e777ef0329a802b879f888b5879bc	# show a detailed account for a specific commit - by specifying is unique commit HASH. (I think by default it will show result for the very LAST commit).
git diff	# shows difference between files in the volatile/working direcory and what is currently in the STAGING-area.
git restore index.js	# RESTORES changes to the WORKSPACE back to what they were in the STAGING-AREA.

AMMEND COMMITS - - 00:38:01
===========================
#
git commit --amend -m "ädded body {} in main.css"	# FIX a screwed up message to the last commit
#

GITHUB - 00:41:00
=================
At the very end is where we sign up to GITHUB if we don't already have an account.

CREATE [GITHUB] REPO - 00:45:00
===============================

git branch	# tells u what branch ur on in ur local machine.
git branch -M main	# Renames ur current local branch to 'main' - EG from 'master' to 'main' (which we did in preparation for moving our local 'master' branch to out GITHUB 'main' branch,
	# çuz fr sume fing reason GITHUB decided to rename the remote master branch from master to main.

git push -u origin main		# PUSH from our local repository to remote (EG github) repository.
#
# MEANING of the git push parameters used here:
# -u origin		take the files from the current LOCAL branch...
# main			name of the REMOTE branch to push the files to. 
#
# When I originally issue this command - I get the following error:
## fatal: 'origin' does not appear to be a git repository
## fatal: Could not read from remote repository.
## Please make sure you have the correct access rights
## and the repository exists.
#
# At time 50:25 in the course I must trawl through a chapter "SSH KEYS SETUP" to resolve security issues.
#

SSH KEYS SET UP - 00:50:24
==========================

# WITHIN THE PROJECT, @top-right corner, click the icon/avatar, then click settings.
# click "SSH and GPG keys"
# We need to generate a public and private SSH keys for our account; We associate the publik-key with our account, we use the private kqey to PUSH into our repository.
# Under SSH-KEYS I see "There are no SSH keys associated with your account." - apparently I never needed them before.
# Click on GENERATING SSH KEYS LINK.
# Click on Generating a new SSH key and adding it to the ssh-agent.
# Look at the directions in Generating a new SSH key. I don't have Git-Bash per-se, and will try to make do without it.
# The following stalled within CYGWIN, so I did it within the WINDOWS command line - I leave any prompts as default-or-empty (I use the -P "" param because sometimes this command hangs without it):
$ ssh-keygen -t ed25519 -C "weingartena@gmail.com" -P ""
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\weing/.ssh/id_ed25519):
Your identification has been saved in C:\Users\weing/.ssh/id_ed25519.
Your public key has been saved in C:\Users\weing/.ssh/id_ed25519.pub.
The key fingerprint is:
SHA256:gPcxqJTbhqe9fI8jpvOkuqgJ7U8jonXre9KpHO0EMFc weingartena@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
|      E          |
|     + .         |
|  o = + o        |
|   = * o o       |
|    = + S        |
| .   B           |
|o + *.=.         |
|o* =oX*.o.       |
|* +=XX=o.o.      |
+----[SHA256]-----+

# We next move on to follow the section "Adding your SSH key to the ssh-agent"
$ eval "$(ssh-agent -s)"
unable to start ssh-agent service, error :1058
# Above, I am trying to run something called "ssh-agent" manually in the background, and am getting an error... Maybe Windows 10 already runs it automatically by default. Will see.
# Add the private SSL key to the ssh config file: (for me the file did not previously exist, and came up as empty):
vi "C:\Users\weing/.ssh/config"
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile "C:\Users\weing/.ssh/id_ed25519"
# And now - add the SSH private key to the ssh-agent:
ssh-add -K "C:\Users\weing/.ssh/id_ed25519"

# ALTERNATIVELY:
mkdir ~/.ssh
touch ~/.ssh/config
vi " ~/.ssh/config
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile "C:\Users\weing/.ssh/id_ed25519"
# And now - add the SSH private key to the ssh-agent:
ssh-add -K "C:\Users\weing/.ssh/id_ed25519"

# ... A lot of stuffing around, a bit much to document...

# NOW we add the SSH key to our GITHUB account (before we were just adding a private key to our dev machine).
# GOTO the link "Adding a new SSH key to your GitHub account.".

GIT PUSH - 00:56:17
===================

# Now do again, and we still get:
$ git push -u origin main
fatal: 'origin' does not appear to be a git repository
fatal: Could not read from remote repository.

# Now do the following, and we are OK:
$ git remote add origin https://github.com/CobaltSoixante/learning-git

### GIT PUSH - 00:56:15
weing@DESKTOP-D0QKA9O /cygdrive/d/MyOtherProjects/learning-git
$ git push -u origin main

Enumerating objects: 13, done.
Counting objects: 100% (13/13), done.
Delta compression using up to 8 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (13/13), 1.74 KiB | 445.00 KiB/s, done.
Total 13 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), done.
To https://github.com/CobaltSoixante/learning-git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.

# After doing the above, after any changes just a 'git push' will suffice, EG:
#Make changes
git add .
git commit -m "..."
git push

### GIT PULL - 01:00:52
# After adding README.md on the REMOTE repository (using the create-README.md-file button), I do the following on my LOCAL repository to PULL it in to LOCAL repository AND WORKSPACE:
git pull

#===================================================================

### BRANCHES (1:06:00-or-01:06:37 / 2:09:00)
Best practice: don't work directly on main/master branch! - Create a 'feature-a' branch, do yoour stuff, and the merge back into master.

### WORKING WITH BRANCHES (1:06:00-or-01:09:09 / 2:09:00)

git branch			# check which LOCAL branch you are on.
git branch feature-a		# CREATE a new branch from the CURRENT branch you are using (seems to stay on the same current branch...)
git checkout feature-a 		# goto the branch u wanna get to
# Do any work U want on the branch.
git push -u origin feature-a	# takes the CURRENT branch, and uploads it to a feature=a branch on the REMOTE.

git branch			# check which LOCAL branch you are on.
git branch -r			# check which branch ur on in REMOTE
git branch -a			# check ALL branches ur on
git checkout -			# alternates bewteen the current branch and the branch we were previously on.

ALTERNATIVE WAY OF CREATING BRANCH FROM main (less steps)
git chechout main		# go back to main branch.
git checkout -b to-delete	# CREATE new branch (will AUTOMATICALY switch to new branch).
git branch -d to-delete		# delete a branch (if this is our CURRENT branch we will get an error).

#===================================================================

### MAIN = MASTER (01:17:35)
# Github (under MS) recently renamed master to main

#===================================================================

### PULL REQUESTS (01:18:16)

[PULL] REQUEST at the github REMOTE LEVEL!

In a corporate environment we DO NOT work on the main brach.
We create a branch named feature-A, feature-B, etc, work on it, commit it, push it to the REMOTE -
and raise a PULL REQUEST -
and select a reviewer from "corporate" (on the REMOTE screen) to merge it to the MAIN for us.

#===================================================================

### MERGING PR'S [PULL REQUESTS] (01:19:17)

# BAD PRCTICE:
# LOCALLY: FROM THE local 'main' branch - merge my 'feature-a' branch into the 'main' branch:
git merge feature-a	# Merge the branch 'feature-a' INTO the branch I am CURRENTLY on (may typically be 'main').
# ABOVE: bad practice. Good practice - see below.

#===================================================================

WORKFLOW:
*. NEVER PUSH to the main/master branch directly.
1. PULL the latest changes from REMOTE 'main' to my LOCAL 'main' repository.
2. git checkout -b newBranchName	# create a new branch LOCALLY.
3. Work on that new branch LOCALLY with all new features, etc...
*. Periodically - push my branch to the REMOTE so I don't lose my changes accidentally.
4. Every day-or-two - "REBASE" my LOCAL main from the "REMOTE", so the corporate/community project doesn't ëscape my grasp.
5. On REMOTE: WHEN I'M READY: Raise [PULL-REQUEST] on REMOTE so my final PUSH-brnch can be reviewed.
6. On REMOTE: [Merge Pull Request] (done by reviewer)
7. [On REMOTE - typically u may DELETE the newBranchName, because ur done with it]
*. On LOCAL - if u do git log [--oneline]  from main(!) branch u wont see the change yet becuz u didn't PULL...
8. On LOCAL: ensure ur in main branch and do "git pull" to get the new merged "main" from REMOTE.
*. Do git log now and ul see it.
*. [On LOCAL - u can now delete the newBranchName from the machine, just as we did on the server: git branch -d feature-a]

#===================================================================

WORKFLOW (revisited - 1:25:50)
1. PULL the latest changes from REMOTE 'main' to my LOCAL 'main' repository. ('git pull' from LOCAL 'main' branch).
2. Create new branch: git -b newBranchName
3. Start working on the feature from the new branch, LOCALLY COMMIT from time to time...
4. Every day or two REBASE from the REMOTE master/main - so I don't go out of sync with the rest of the world...
5. ... NOW, before I REBASE master/main LOCALLY, I am well off to first "SQUASH" my LOCAL commits in my branch first - so I have one single commit: this way, IF I have CONFLICTS - I only need to resolve them for 1 single commit (and not 10 individual commits)...
6. ... Then I REBASE master/main (LOCALLY)...
7. ... I then STASH my COMMIT (LOCALLY), bring all my changes from master to main, and put my COMMIT on top of it...
8. ... Finally: PUSH to REMOTE, discuss with peers, yadda yadda, merge my commit to the REMOTE main/master branch.

#===================================================================

DEALING WITH CONFLICTS (1:28:38) and MERGING CONFLICTS (1:34:46)
*. Say we made changes to index.html on our LOCAL feature-xyz branch (doing this with VS-CODE is nice because it color-codes conflicts as we go along). And some idiot made conflicting changes and "beat us to it"and checked them into the REMOTE feature-xyz branch...
*. ... Now we (me) have to PULL the changes from REMOTE into our LOCAL (git pull).
*. We now LOCALLY have an annotated copy of index.html with guidelines for resolving/merging the conflict (presumably this is non-destructive - because we already have a LOCAL commit on our machine of our desired content for this file).

#===================================================================

GIT REBASE (intro: 1:40:54; detail: 1:42:08; recap: 1:52:20)

*. REBASE is a process of bringing the changes in the REMOTE (typically the master/main) - and imposing them upon the LOCAL BRANCH you are working on.
*. We continue working with LOCAL branch 'feature-xyz' that we created last section.

*. The corporate/REMOTE master/main has chenged: we need to incorporate those changes into our LOCAL feature-xyz branch (this is something we do periodically - just to keep touch with corporate)
   Look at this as: we bring in REMOTE/corporate master/main, and try to impose this on our LOCAL 'feature-xyz'branch:
   Will work smoothly UNLESS there are conflicts, and then we must resolve them...
*. ...Conceptually, is like this: we work on our LOCAL/dev branch, and want to periodically resync/REBASE IT with the REMOTE/CORPORATE main/master branch (so we are not out of touch with CORPORATE).
   So, we REBASE: we take everything from REMOTE/CORPORATE main/master to our LOCAL/dev branch, and REMOTE/CORPORATE becomes our guideline! -
   - We then go through the process of RE-SUPERIMPOSING our own recent LOCAL/dev changes  (IE 'since last REBASE') on what is now a current [LOCAL] snapshot of REMOTE/CORPORATE.
# From our LOCAL 'feature-xyz' branch:
git pull -r origin main
# or:
git pull --rebase origin main
# I think 'origin' means our current LOCAL branch, and 'main' is the REMOTE branch we are rebasing from. I suppose that 'main' is the norm, but that u may specify a different REMOTE branchname (typically identical to your local) in the crazy case where several teal members are attacking the same branchName.

#- - - - - - - - -

# REPEATEDLY do the following 3 steps until the LAST step ('git rebase --continue') says "Seccessfully rebased and updated ..."
## via EDITOR: RESOLVE any conflicts LOCALLY (EG via visual code)
git add . # Restage any conflicts u resolved manually.
git rebase --continue # rebase conflict #1 and 'continue' rebasing if necessary.
## IN REALITY - when u want to REBASE u may want to first "sqaush" (stash?) al you branch commits into a single commit so u dont have to repeate the above multiple times.
   This may(?) spare u the step that follows.

# FINALLY, At the end of this our REMOTE branch (feature-xyz) STILL won't contain the material we ORIGINALLY 'pull --rebased'd in from CORPORATE (though it will contain all our CONFLICT resolutions, IE the original material we ADDED to the LOCAL branch). To resolve this:
git push --force

# WHEN WE ARE READY to check into REMOTE/CORPORATE/master main -
# the simplest flow of events at the LOCAL will be:
git add .
git commit -m "comment"   # remember: this is only a LOCAL operation
git push
# goto SERVER/CORPORATE website and do [PULL REQUEST]: (for some reason we did not perform this at the end of the lesson - only ALMOST did it, without confirming).

#===================================================================

GIT CLIENTS (1:53:59)

# The guy doesn't use any, but mentions: GitHub DeskTop, SourceTree, Visual code
GitHub DeskTop  [is the official one]
SourceTree
most IDE's have GIT integration built in, EG: VS Code...

#===================================================================

GITPOD (1:57:42)

# I dont get a GITPOD bitton: mebbe cuz I dont have the jetbrains plugins he's got.
  Its about having a IDE on the web (including VS-CODE).
# I get ~something if I prepend 'gitpod.io/#' to my github repository URL: dunno what it is.
# dont think I need this thing: gives u a VISUAL Code IDE on the cloud - for if u have a crap PC?

#===================================================================

BUILDING YOUR OWN PORTFOLIO (2:00:35)

READ.md file - has its own syntax. U need to goto another link to learn it.

#===================================================================

EXPLORING GITHUB (2:06:50)

#===================================================================

OPEN SOURCE SOFTWARE (2:13:53)

At top  click [EXPLORE] - u get to all the repositories on GITHUB.

ur project - if open - should have a "LICENSE" file. Has formatting rules: 2B explored.

#===================================================================

OPEN SOURCE SOFTWARE (2:19:44)

