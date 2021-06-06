#	WORKSPACE			STAGING-AREA			LOCAL-REPOSITORY
#									log
#									show	
#                                       		-commit->
#			-add-> 
#					rm
#			<-diff->
#			<-restore-
#
git init .	# Create new git repository at current directory.
git status	# Shows current git branch and other stuff about the branch.
git add index.html	# Added index.html to the staging area.
git rm --cached index.html	# Remove index.html from the staging area. DOES NOT remove the physical file  :-)  .
git add .	# Add all files in staging area AND downwards...
git rm -r --cached .	#  Remove all files in staging area and downwards (the -r does the downwards/recursively bit).
git add -A	# Will add your ENTIRE workspace to your stage directory - Up AND Down - even if you are inside a sub-directory (eg ./test).
git commit -m "bootstrap project"	# Commit [locally] all mofified files in the staging area.
git log					# gives a terse commit history, including commit HASH, MESSAGE, DATE-TIME STAMP.
git show 38b3070a450e777ef0329a802b879f888b5879bc	# show a detailed account for a specific commit - by specifying is unique commit HASH. (I think by default it will show result for the very LAST commit).
git diff	# shows difference between files in the volatile/working direcory and what is currently in the STAGING-area.
git restore index.js	# RESTORES changes to the WORKSPACE back to what they were in the STAGING-AREA.
