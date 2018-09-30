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

It will open your editor and you can choose what you want to do with each
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

