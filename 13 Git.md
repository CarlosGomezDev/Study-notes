`2020-01-15 Git 19:30`
# Git

### Delete commit history, keep latest code version.
Checkout <br>
`git checkout --orphan latest_branch` <br>
Add all the files <br>
`git add -A` <br>
Commit the changes <br>
`git commit -am "Initial Commit"` <br>
Delete the branch <br>
`git branch -D main` <br>
Rename the current branch to main <br>
`git branch -m main` <br>
Finally, force update your repository <br>
`git push -f origin master` <br>