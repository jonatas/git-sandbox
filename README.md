#  Git start

```
mkdir project
cd project
git init
```

## Create some file

`README.md` is created with initial content.

## Add file

Using progressive mode.

`git add -p`

⋊> ~/c/t/git-sandbox on master ⨯ git add -p                                                                                                                                         21:13:55
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
⋊> ~/c/t/git-sandbox on master ⨯ git st                                                                                                                                             21:14:00
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   README.md
```

## Check staged files

Confirming about the extra lines that are going to the commit:

```
⋊> ~/c/t/git-sandbox on master ⨯ git diff --staged                                                                                                                                  21:14:14
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
⋊> ~/c/t/git-sandbox on master ⨯ git reset README.md                                                                                                                                21:14:18
Unstaged changes after reset:
M	README.md
⋊> ~/c/t/git-sandbox on master ⨯ git diff                                                                                                                                           21:14:26
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
⋊> ~/c/t/git-sandbox on master ⨯ git add -p                                                                                                                                         21:14:28
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
⋊> ~/c/t/git-sandbox on master ⨯ git diff                                                                                                                                           21:14:39
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
⋊> ~/c/t/git-sandbox on master ⨯ git diff --staged                                                                                                                                  21:14:44
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

## Amend current commit

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


