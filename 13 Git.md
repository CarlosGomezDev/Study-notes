`2020-01-15 Git 19:30`
# Git

### Delete commit history, keep latest code version.
Checkout
`git checkout --orphan latest_branch`
Add all the files
`git add -A`
Commit the changes
`git commit -am "Initial Commit"`
Delete the branch
`git branch -D main`
Rename the current branch to main
`git branch -m main`
Finally, force update your repository
`git push -f origin master`