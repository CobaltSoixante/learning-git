git init .	# Create new git repository at current directory.
git status	# Shows current git branch and other stuff about the branch.
git add index.html	# Added index.html to the staging area.
git rm --cached index.html	# Remove index.html from the staging area. DOES NOT remove the physical file  :-)  .
git add .	# Add all files in staging area AND downwards...
git rm -r --cached .	#  Remove all files in staging area and downwards (the -r does the downwards/recursively bit).
