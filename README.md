# Git init

```
mkdir project
cd project
git init
```

# Git add

`README.md` is created with initial content.

## Git add `-p` or `--progressive`

Using progressive mode.

`git add -p`

```diff --git a/README.md b/README.md
index 34e1bdd..ed610a0 100644
--- a/README.md
+++ b/README.md
@@ -11,3 +11,10 @@ git init
 `README.md` is created with initial content.

 ## Add file
+
+Using progressive mode.
+
+
+`git add -p`
+
+
Stage this hunk [y,n,q,a,d,e,?]? y
<stdin>:14: new blank line at EOF.
+
warning: 1 line adds whitespace errors.
```

## Reset staged files

Look in the last line git is warning about whitespace errors.
By a mistake I added two extra blank lines and the changes are tracked but not
commited yet.

```
⋊> ~/c/t/git-sandbox on master ⨯ git st
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   README.md
```

## Check staged files

Confirming about the extra lines that are going to the commit:

```
⋊> ~/c/t/git-sandbox on master ⨯ git diff --staged
diff --git a/README.md b/README.md
index 34e1bdd..ed610a0 100644
--- a/README.md
+++ b/README.md
@@ -11,3 +11,10 @@ git init
 `README.md` is created with initial content.

 ## Add file
+
+Using progressive mode.
+
+
+`git add -p`
+
+
```

Reseting the changes will not erase what you did. Just discard the git entries:

```
⋊> ~/c/t/git-sandbox on master ⨯ git reset README.md
Unstaged changes after reset:
M	README.md
⋊> ~/c/t/git-sandbox on master ⨯ git diff
diff --git a/README.md b/README.md
index 34e1bdd..ed610a0 100644
--- a/README.md
+++ b/README.md
@@ -11,3 +11,10 @@ git init
 `README.md` is created with initial content.

 ## Add file
+
+Using progressive mode.
+
+
+`git add -p`
+
+
```

## Edit partials with `--progressive`

Using progressive mode you can use `e` option to edit the changes and remove
what you don't want:

```
⋊> ~/c/t/git-sandbox on master ⨯ git add -p
diff --git a/README.md b/README.md
index 34e1bdd..ed610a0 100644
--- a/README.md
+++ b/README.md
@@ -11,3 +11,10 @@ git init
 `README.md` is created with initial content.

 ## Add file
+
+Using progressive mode.
+
+
+`git add -p`
+
+
Stage this hunk [y,n,q,a,d,e,?]? e
```

Using `e` will open your editor to make the changes and remove the undesired
changes, but they remains in the original file:

```
⋊> ~/c/t/git-sandbox on master ⨯ git diff
diff --git a/README.md b/README.md
index 7a36e0e..ed610a0 100644
--- a/README.md
+++ b/README.md
@@ -16,3 +16,5 @@ Using progressive mode.


 `git add -p`
+
+
```

And only the changes I want are staged:

```
⋊> ~/c/t/git-sandbox on master ⨯ git diff --staged
diff --git a/README.md b/README.md
index 34e1bdd..7a36e0e 100644
--- a/README.md
+++ b/README.md
@@ -11,3 +11,8 @@ git init
 `README.md` is created with initial content.

 ## Add file
+
+Using progressive mode.
+
+
+`git add -p`
```

If you have multiple files, try [git add -i]( https://git-scm.com/book/en/v2/Git-Tools-Interactive-Staging). 

## Git commit `-v`

Using `git commit -p` from this point will open your favorite editor with the followig details:

    git commit -v

Consider the first line what I added as  the commit message.

```git
Add commit -p

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Sat Sep 29 21:57:21 2018 -0300
#
# On branch master
# Your branch is ahead of 'origin/master' by 1 commit.
#   (use "git push" to publish your local commits)
#
# Changes to be committed:
#committedmodified:   README.md
#
# Changes not staged for commit:
#commitmodified:   README.md
#
# ------------------------ >8 ------------------------
# Do not modify or remove the line above.
# Everything below it will be ignored.
diff --git a/README.md b/README.md
index 34e1bdd..7a36e0e 100644
--- a/README.md
+++ b/README.md
@@ -11,3 +11,8 @@ git init
 `README.md` is created with initial content.
  
   ## Add file
   +
   ++Using progressive mode.
   +
   ++
   +`git add -p`
```

Saving the message and closing the editor will make the commit right after close the editor.

```
[master 5c0e0f2] Add commit -p
 1 file changed, 5 insertions(+)
```

## Git commit `--amend`

You can use `--amend` option to fix your current commit message:

    $ git commit --amend -m "Another commit message"

Of you can do more changes and even keep the same message using `--no-edit`:

    $ git add README.md 
    $ git commit --amend --no-edit

Both cases will rewrite the last commit.

```
 [master 8efea81] Add commit -p
  Date: Sat Sep 29 21:57:21 2018 -0300
   1 file changed, 5 insertions(+)
```

## Git commit `--fixup`

Fixup can be useful for creating partial commits that belongs from previous
implementation.

Checking the commits log:


```
git l
* 8f9dc6f - (18 seconds ago) Remove time track - Jônatas Davi Paganini (HEAD -> master)
* 76c0158 - (8 minutes ago) Add more about git first steps - Jônatas Davi Paganini (origin/master)
* 8efea81 - (20 minutes ago) Add commit -p - Jônatas Davi Paganini
* 274a2a1 - (77 minutes ago) First commit :tada: - Jônatas Davi Paganini
 ```

Let's consider we made some changes and we want to put them in a specific commit.

```
git add README.md
git commit --fixup 8efea81
```

And now we have a new commit:

```
git l
* 2d49541 - (4 seconds ago) fixup! Add commit -p - Jônatas Davi Paganini (HEAD -> master)
* 7671b4e - (26 minutes ago) Remove time track - Jônatas Davi Paganini
* 76c0158 - (34 minutes ago) Add more about git first steps - Jônatas Davi Paganini (origin/master)
* 8efea81 - (45 minutes ago) Add commit -p - Jônatas Davi Paganini
* 274a2a1 - (2 hours ago) First commit :tada: - Jônatas Davi Paganini<Paste>
```

# Git rebase 

Now we have a fixup and we can group them into the previous commit. We can start
rebasing from the first commit using the interactive mode to choose what we want
to squash:

## Git rebase `-i`

With interactive mode, it will open your editor and you can choose what you want to do with each
message: 

```
pick 8efea81 Add commit -p
fixup 2d49541 fixup! Add commit -p
pick 76c0158 Add more about git first steps
pick 7671b4e Remove time track
```

You can see it suggests to `fixup` the commit we marked with `--fixup`.

If you simply save the file and quit it will rewrite your commits following the
order stated previously.

The current rebase can fail and you will see a message warning about conflicts.

```
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
error: could not apply 239449e... fixup! Add commit -p

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".

Could not apply 239449e... fixup! Add commit -p
```

You can open the `README.md` file and fix the errors to continue the rebase or
abort and start again.

Learn more about rebase and squash [here](https://robots.thoughtbot.com/autosquashing-git-commits).

# Git pull

Git pull automatically download commits but it also create extra merge commits
for each fetch.

    $ git pull origin master

## Git pull `-r`

Using pull with `--rebase` or `-r` option allow to receive new commits without
poluting the commit history.

Rebase rewrite your commits in the top of the branch that you're using. It can
be useful to keep your branch up to date with master and for getting the latest
news from master you can simply rebase from master branch.

    $ git pull -r origin master

In case you're working with teammates in the same branch you can rebase from
others people work.

    $ git checkout branch-name
    $ git pull -r origin branch-name

Or from another person fork:

    $ git remote add friend git@fork-url
    $ git pull -r friend branch-name

# Git push

Git push allow you to send commits to a remote git repository.

## Git push `-u`

The `-u` option will automatically track the remote branch with the local branch
and you don't need to  say the remote and the branch name everytime.

    $ git checkout -b new-branch
    $ git push -u origin new-branch

Now the branch is tracked and you can simply say `git push` or `git pull`.

For deleting a branch from a remote source the branch you also use pull with the following syntax:

    $ git push origin :new-branch

For deleting the branch locally, use `git branch -D branch-name`

# Git fetch

Use git fetch to checkout other people work from the remote. Example:

    $ git fetch origin

## Git fetch `--prune`

If you work with a big team and multiple people are pushing branches everyday,
use `--prune` option can be useful. It deletes local references to remote branches
that have been deleted in the remote.

# Git checkout

Git checkout switch between branches or restore working tree files.

* Git checkout `-b` to create a new branch

## Restore to a specific commit

Let's say you messed with something and need to rollback the latest 3 commits
and make it your last commit in a branch.

You can use git reflog to try something.

## Git reflog

    $ git reflog

It will bring a list of commits and all actions executed in the local host.

Find the commit reference and checkout the HEAD.

    git co HEAD@{3}
    git branch -D my-branch
    git co -b my-branch
