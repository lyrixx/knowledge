# Git tips

Resources:

* [genomewiki](http://genomewiki.ucsc.edu/index.php/Resolving_merge_conflicts_in_Git)
* [Git scm](http://git-scm.com/book)
* [Justin Hileman](http://justinhileman.info/article/changing-history/)
* [Daniel Kummer](http://danielkummer.github.io/git-flow-cheatsheet/)
* [Git Cheatsheet](http://ndpsoftware.com/git-cheatsheet.html)
* [Resources for learning Git](http://speckyboy.com/2013/06/03/resources-for-learning-git)
* [Git tips from the pros](http://net.tutsplus.com/tutorials/tools-and-tips/git-tips-from-the-pros/)

## Solving merge conflicts

When merging with Git, conflicts can happen. To resolve them, simply:

1. find the conflicted files with `git status`
   (they'll have the `unmerged` mention)
2. edit the conflicted files and make the necessary modifications
3. `git add` the resolved files
4. `git commit` to finish the merge

## Managing your branches

1. listing existing branches: `git branch -avv`;
2. creating a new branch and switch to it: `git checkout -b <branch-name>`
3. renaming the current branch: `git branch -m <current-branch-name> <new-branch-name>`
4. pushing the branch and tracking it: `git push -u <remote> <branch-name>`
5. creating a branch from a remote one and track it: `git checkout -t <remote>/<branch-name>`
6. tracking a remote branch: `git branch --set-upstream <branch-name> <remote>/<branch-name>`
7. removing the remote branch: `git push <remote> :<branch-name>` (note the `:` before the branch name)
8. removing a local branch: `git branch -d <branch-name>` (won't remove unmerged branches)
9. removing branches that doesn't exist anymore on the repository: `git fetch -p`
10. finding merged/unmerged branches: `git branch --merged; git banch --no-merged`

## Managing your tags

1. listing existing tags: `git tag`
2. creating a new tag: `git tag -a <tag-name> -m '<message>'`
3. pushing the tag: `git push <remote> <tag-name>`
4. creating an alias: `git tag <existing-tag-name> <new-tag-name>`
5. removing a remote tag: `git push <remote> :<tag-name>` (note the `:` before the tag name)
6. removing a local tag: `git tag -d <tag-name>`
7. renaming a tag: create an alias and remove the old tag
8. moving a tag to the current commit: `git tag -f <tag-name>`

## Managing ref updates (checkout, reset, commit, merge, etc)

1. checking the history of ref updates: `git reflog [show <branch>]`
2. undoing last ref update: `git reset HEAD@{1}`

Source: [Stack overflow: Undoing git reset](http://stackoverflow.com/questions/2510276/undoing-git-reset)

## Splitting a commit

1. select the commits: `git rebase -i HEAD~<number>`
2. mark the commit: change `pick` to `edit`
3. save and quit the editor
4. undo the commit: `git reset HEAD^`
5. stage and commit: `git add <file>; git commit -m <message>`
6. apply the split: `git rebase --continue`

Source: [Git scm: Splitting a commit](http://git-scm.com/book/en/Git-Tools-Rewriting-History#Splitting-a-Commit)

## Join last commits into the previous one

1. select the commits: `git rebase -i HEAD~<number>`
2. mark the commits: change `pick` to `fixup`

Source: [Git scm: Squashing commits](http://git-scm.com/book/en/Git-Tools-Rewriting-History#Squashing-Commits)

## Reorder commits

1. select the commits: `git rebase -i HEAD~<number>`
2. change the order of the lines

Source: [Git scm: Reordering commits](http://git-scm.com/book/en/Git-Tools-Rewriting-History#Reordering-Commits)

## Modify commit

:warning: These tips work for un-propagated commits

### Change the last commit message

``git commit --amend``

### Modify specific commit

1. start rebase: `git rebase -i <number>^`
2. mark the commit: change `pick` to `edit`
3. edit your files
4. add them `git add <filepattern>`
5. `git commit --amend`
6. And return to the head with `git rebase --continue`

## Commit part of a file

1. select the file: `git add -p <file>`
2. choose what to do:
   * accept the chunk: hit `y`
   * reject the chunk: hit `n`
   * select part of the chunk: hit `e`, or `s` if available
3. save and quit the editor
4. commit: `git commit -m <message>`

Source: [Git scm: Staging patches](http://git-scm.com/book/en/Git-Tools-Interactive-Staging#Staging-Patches)

## Reset a local branch from remote branch

1. start fetch: `git fetch <remote>`
2. reset from the chosen remote: `git reset --hard <remote>/<branch>`
3. check you have no differences between the two branches: `git diff <branch>...<remote><branch>` should respond nothing.

Source: [Git scm: Reset history](http://git-scm.com/docs/git-reset)
