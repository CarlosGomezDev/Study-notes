`2020-01-15 Git 19:30`

# Git

## View local commits

To view commit history on local copy, this might or might not be in sync with github
`git reflog` <br>
`git log` <br>
`git log --oneline` <br>

## Delete Local Branch

`git branch -d [branch_name]`

## Delete brach on github and reupload local as new branch

`git push origin :[branch_name]`, notice the `<empty>:[branch_name]`, this will push `<emptyness>` to github<br>
`git branch -m [branch_name] [new_brach_name]`, if you want to rename local brach before pushing<br>
`git push origin [branch_name]`, push local branch to github<br>

## Check git status on all sub-folders

`find . -type d -name '.git' | while read dir ; do sh -c "cd $dir/../ && echo -e \"\nGIT STATUS IN ${dir//\.git/}\" && git status -s" ; done`

## Remove commit from github

`git reset --hard [sha1]` choose the commit you want to be on, this downgrades local copy
`git reset [sha1]` choose the commit you want to be on, this downgrades local copy

![](src/img/13-1.png)

- The difference between them is to change or not change head, stage (index), working directory.
  - `git reset --hard` will change **head**, **index/stage** and **working directory**.
  - `git reset --soft` will change **head** only. No change to _index/stage_, or _working directory_.

`git push origin -f` this pushes the downgraded copy to github

## Remove commits from local

`git fetch --all` grab latest github commits
`git reset --hard origin/[branch_name]` downgrade your local "main" branch to whatever github has

## Delete commit history, keep latest code version.

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
