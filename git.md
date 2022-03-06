![](assets/images/git.gif)

# Git
### Things learned
* Commit locally often
* Create new branches for each feature


### General
Check the status

	git status

Check the branches

	git branch

### Git Push coasssst

	git add -A
	git commit -m 'commit message’
	git push origin master

### Branches
To make a new branch

	git checkout -b new-branch

Go back to master branch and merge
	
	git checkout master
	git merge new-branch

And then to delete the branch

	git branch -d new-branch

(`-d` will work if the commits are up-to-date. If not you have to use `-D` to force the delete)

### Multiple Accounts
	git init
	git config user.name altuser
	git config user.email "altemail"
	git add .
	git commit -m "init"
	git branch -M main
	git remote add origin github.com-altuser:altuser/altrepo.git
	git push -u origin main

	git init
	git config user.name altuser
	git config user.email "altemail"
	git add .
	git commit -m "init"
	git branch -M main
	git remote add origin https://github.com/githubuser/altrepo.git
	git remote set-url origin github.com-altuser:githubuser/altrepo.git
	git push -u origin main

### Mistakes
If I have to force a push

	git push origin master -f

Reverting commits

	git revert -n HEAD~3..HEAD  # prepare a new commit reverting last 3 commits
	git commit -m 'commit message'
	git push origin master  # regular push

If there is a caching issue

	git filter-branch -f --index-filter "git rm -rf --cached --ignore-unmatch FOLDERNAME" -- --all