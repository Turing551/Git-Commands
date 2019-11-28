Git Commands
============


### Getting & Creating Projects

| Command | Description |
| ------- | ----------- |
| `git init` | Initialize a local Git repository |
| `git clone ssh://git@github.com/[username]/[repository-name].git` | Create a local copy of a remote repository |

### Basic Snapshotting

| Command | Description |
| ------- | ----------- |
| `git status` | Check status |
| `git add [file-name.txt]` | Add a file to the staging area |
| `git add -A` | Add all new and changed files to the staging area |
| `git commit -m "[commit message]"` | Commit changes |
| `git rm -r [file-name.txt]` | Remove a file (or folder) |

### Branching & Merging

| Command | Description |
| ------- | ----------- |
| `git branch` | List branches (the asterisk denotes the current branch) |
| `git branch -a` | List all branches (local and remote) |
| `git branch [branch name]` | Create a new branch |
| `git branch -d [branch name]` | Delete a branch |
| `git push origin --delete [branchName]` | Delete a remote branch |
| `git checkout -b [branch name]` | Create a new branch and switch to it |
| `git checkout -b [branch name] origin/[branch name]` | Clone a remote branch and switch to it |
| `git checkout [branch name]` | Switch to a branch |
| `git checkout -` | Switch to the branch last checked out |
| `git checkout -- [file-name.txt]` | Discard changes to a file |
| `git merge [branch name]` | Merge a branch into the active branch |
| `git merge [source branch] [target branch]` | Merge a branch into a target branch |
| `git stash` | Stash changes in a dirty working directory |
| `git stash clear` | Remove all stashed entries |

### Sharing & Updating Projects

| Command | Description |
| ------- | ----------- |
| `git push origin [branch name]` | Push a branch to your remote repository |
| `git push -u origin [branch name]` | Push changes to remote repository (and remember the branch) |
| `git push` | Push changes to remote repository (remembered branch) |
| `git push origin --delete [branch name]` | Delete a remote branch |
| `git pull` | Update local repository to the newest commit |
| `git pull origin [branch name]` | Pull changes from remote repository |
| `git remote add origin ssh://git@github.com/[username]/[repository-name].git` | Add a remote repository |
| `git remote set-url origin ssh://git@github.com/[username]/[repository-name].git` | Set a repository's origin branch to SSH |

### Inspection & Comparison

| Command | Description |
| ------- | ----------- |
| `git log` | View changes |
| `git log --summary` | View changes (detailed) |
| `git diff [source branch] [target branch}` | Preview changes before merging |

### The difference between git reset --mixed, --soft, and --hard

When you modify a file in your repository, the change is initially unstaged. In order to commit it, you must stage it—that is, add it to the index—using `git add`. When you make a commit, the changes that are committed are those that have been added to the index.

`git reset` changes, at minimum, where the current branch `(HEAD)` is pointing. The difference between `--mixed` and `--soft` is whether or not your index is also modified. So, if we're on branch `master` with this series of commits:

`- A - B - C (master)`

`HEAD` points to `C` and the index matches `C`.

When we run `git reset --soft B`, `master` (and thus `HEAD`) now points to `B`, but the index still has the changes from `C`; `git status` will show them as staged. So if we run git commit at this point, we'll get a new commit with the same changes as `C`.

Okay, so starting from here again:

`- A - B - C (master)`

Now let's do `git reset --mixed B`. (Note: `--mixed` is the default option). Once again, `master` and `HEAD` point to B, but this time the index is also modified to match B. If we run `git commit` at this point, nothing will happen since the index matches HEAD. We still have the changes in the working directory, but since they're not in the index, git status shows them as unstaged. To commit them, you would git add and then commit as usual.


And finally, `--hard` is the same as `--mixed` (it changes your `HEAD` and index), except that `--hard` also modifies your working directory. If we're at `C` and run `git reset --hard B`, then the changes added in `C`, as well as any uncommitted changes you have, will be removed, and the files in your working copy will match commit `B`. Since you can permanently lose changes this way, you should always run `git status` before doing a hard reset to make sure your working directory is clean or that you're okay with losing your uncommitted changes.

### In the simplest terms:

`--soft`: **uncommit changes**, changes are left staged (index).

`--mixed` (default): **uncommit + unstage** changes, changes are left in working tree.

`--hard`: **uncommit + unstage + delete** changes, nothing left.

### Difference between git add, commit, push

1. `git add` adds your modified files to the queue to be committed later. Files are not committed


2. `git commit` commits the files that have been added and creates a new revision with a log... If you do not add any files, git will not commit anything. You can combine both actions with git commit -a


3. `git push` pushes your changes to the remote repository.
