# This course learnt from:
# Amigoscode - Git and GitHub Tutorial For Beginners | Full Course [2021] [NEW]
# https://www.youtube.com/watch?v=3fUbBnN_H2c&t=2753s

# I don't care to "install" GIT right now,  because it comes sorta prepackagaged eith my VISUAL-STUDIO 2019: I just add the following directory to my path:
# C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\IDE\CommonExtensions\Microsoft\TeamFoundation\Team Explorer\Git\cmd

# My initial GIT config commands.
git config --global user.name "CobaltSoixante"
git config --global user.email "weingartena@gmail.com"
git config --global color.ui auto

git config -l	#	List all my configuration parameters.

# Ctrl+L = clear screen
# In GIT a REPOSITORY is simply a COLLECTION of various different VERSIONS of a PROJECT.


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
#												-push->
#
git init .	# Create new git repository at current directory.
git status	# Shows current git branch and other stuff about the branch.
#
git add index.html	# Added index.html to the staging area.
git rm --cached index.html	# Remove index.html from the staging area. DOES NOT remove the physical file  :-)  .
#
git add .	# Add all files in staging area AND downwards...
git rm -r --cached .	#  Remove all files in staging area and downwards (the -r does the downwards/recursively bit).
git add -A	# Will add your ENTIRE workspace to your stage directory - Up AND Down - even if you are inside a sub-directory (eg ./test).
git commit -m "bootstrap project"	# Commit [locally] all mofified files in the staging area.
git log					# gives a terse commit history, including commit HASH, MESSAGE, DATE-TIME STAMP.
git show 38b3070a450e777ef0329a802b879f888b5879bc	# show a detailed account for a specific commit - by specifying is unique commit HASH. (I think by default it will show result for the very LAST commit).
git diff	# shows difference between files in the volatile/working direcory and what is currently in the STAGING-area.
git restore index.js	# RESTORES changes to the WORKSPACE back to what they were in the STAGING-AREA.
#
git commit --amend -m "ädded body {} in main.css"	# FIX a screwed up message to the last commit
#
git branch	# tells u what branch ur on in ur local machine.
git branch -M main	# Renames ur current local branch to 'main' - EG from 'master' to 'main' (which we did in preparation for moving our local 'master' branch to out GITHUB 'main' branch,
	# çuz fr sume fing reason GITHUB decided to rename the remote master branch from master to main.

git push -u origin main		# PUSH from our local repository to remote (EG github) repository.
# When I originally issue this command - I get the following error:
## fatal: 'origin' does not appear to be a git repository
## fatal: Could not read from remote repository.
## Please make sure you have the correct access rights
## and the repository exists.
#
# At time 50:25 in the course I must trawl through a chapter "SSH KEYS SETUP" to resolve security issues.
#
# Withing the project, @top-righnt cornet, click the icon/avatar, then click settings.
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

# Now do again, and we still get:
$ git push -u origin main
fatal: 'origin' does not appear to be a git repository
fatal: Could not read from remote repository.

# Now do the following, and we are OK:
$ git remote add origin https://github.com/CobaltSoixante/learning-git

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

