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

Let's consider we made some changes and we want to put them in a specific commit:

```
 git commit -m "fixup 8efea81 Add commit --progressive"
[master f4dcb2a] fixup 8efea81 Add commit --progressive
 1 file changed, 3 insertions(+), 4 deletions(-)
```

Using `git show` it's possible to see what are the c

    $ git show

```
commit f4dcb2a944d2be4f69e07abc062fec4dfe8c4a0f (HEAD -> master)
Author: Jônatas Davi Paganini <jonatas.paganini@toptal.com>
Date:   Sat Sep 29 22:20:19 2018 -0300
```

    fixup 8efea81 Add commit --progressive

```diff --git a/README.md b/README.md
index 7a6177a..5a47a0e 100644
-## Add file
+## Git add `-p` or `--progressive`
```

    $ git l
```
* f4dcb2a - (7 seconds ago) fixup 8efea81 Add commit --progressive - Jônatas Davi Paganini (HEAD -> master)
* 8f9dc6f - (4 minutes ago) Remove time track - Jônatas Davi Paganini
* 76c0158 - (12 minutes ago) Add more about git first steps - Jônatas Davi Paganini (origin/master)
* 8efea81 - (23 minutes ago) Add commit -p - Jônatas Davi Paganini
* 274a2a1 - (80 minutes ago) First commit :tada: - Jônatas Davi Paganini
```

# Git rebase 

Now we have a fixup and we can group them into the previous commit. We can start
rebasing from the first commit using the interactive mode to choose what we want
to squash:

It will open your editor and you can choose what you want to do with each
message:

```
pick 8efea81 Add commit -p
pick 76c0158 Add more about git first steps
pick 8f9dc6f Remove time track
pick 9c32078 fixup 8efea81 Add commit --progressive
```

You can see it suggests to `pick` the `fixup` message we have in the log. To
automatically fix it with git you can use the `--autosquash` in the rebase
option:





pick 8efea81 Add commit -p
pick 76c0158 Add more about git first steps
fixup 8f9dc6f Remove time track
fixup 9c32078 fixup 8efea81 Add commit --progressive

# Rebase 274a2a1..9c32078 onto 274a2a1 (4 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
#	However, if you remove everything, the rebase will be aborted.
#
#
# Note that empty commits are commented out

