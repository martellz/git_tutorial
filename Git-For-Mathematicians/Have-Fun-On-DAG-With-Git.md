## Git For Mathematicians 2 : Have Fun on DAG with Git

Let's do some hands-on experiments! You absolutely want to see the DAG in action!

First make sure you have installed git. On windows, simple search and download. On linux, use your package manager like `sudo pacman -S git` or `sudo apt-get install git`.

### Create a new repository

```bash
mkdir git-dag # create a new directory
cd git-dag    # enter the directory
git init      # initialize a new git repository
```

#### Adding A Magic Theorem

There is nothing in the repo to play with yet. Let's create a new file, for example maybe you are working with a magic proof.

```bash
echo "Theorem: Some magic is happening here." > magic-proof.md
git status
```

You will see

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	magic-proof.md

nothing added to commit but untracked files present (use "git add" to track)
```

Oh, git tells us that the file is untracked. Let's add it to the staging area and re-run `git status`.

#### Tracking The Magic Theorem

```bash
git add magic-proof.md   # add the file to the staging area
git status
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   magic-proof.md
```

#### Committing The Magic Theorem

Cool, the file is now staged. Let's commit it, so it will appear as a new vertex in our DAG! >w<

```bash
git commit -m "Initial commit: Add magic theorem."
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git commit -m "Initial commit: Add magic theorem"
[master (root-commit) ee464ad] Initial commit: Add magic theorem
 1 file changed, 1 insertion(+)
 create mode 100644 magic-proof.md
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git status
On branch master
nothing to commit, working tree clean
```

### Check Your First Node (Commit)!

Now we have added one vertex (commit) to our DAG. Let's see it!

```bash
git log --graph

# you can also run with --oneline flag to simplify the output
git log --graph --oneline
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git log --graph
* commit ee464ad7f9d00972d4c15c0c8fff6ed92893a625 (HEAD -> master)
  Author: Eiko <eikochanowo@outlook.com>
  Date:   Sun Dec 8 17:56:01 2024 +0000

      Initial commit: Add magic theorem
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git log --graph --oneline
* ee464ad (HEAD -> master) Initial commit: Add magic theorem
```

* See that little dot `*`? That's a vertex in our DAG corresponding to the commit we just made. 

* The commit hash `ee464ad` is the unique identifier for this commit. You can use it to refer to this vertex (commit) in the future.

* The `HEAD -> master` part tells us that we are currently on the `master` branch and that this branch points to the latest commit, which is the vertex in the DAG we just added.

### Create A New Branch

Let's grow our DAG by adding a **new branch**.

```bash
git checkout -b fire-magic
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git checkout -b fire-magic
Switched to a new branch 'fire-magic'
```

You can see that something have changed:

```bash
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git status
On branch fire-magic
nothing to commit, working tree clean

[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git log --graph
* commit ee464ad7f9d00972d4c15c0c8fff6ed92893a625 (HEAD -> fire-magic, master)
  Author: Eiko <eikochanowo@outlook.com>
  Date:   Sun Dec 8 17:56:01 2024 +0000

      Initial commit: Add magic theorem
```

The `HEAD -> fire-magic` part tells us that we are now on the `fire-magic` branch.

Of course we will want to explore some fire magic in this branch.

```bash
echo "Proof: Fire magic is the best magic." >> magic-proof.md
git add magic-proof.md
git commit -m "Add proof using fire magic."
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ echo "Proof: Fire magic is the best magic." >> magic-proof.md
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git add magic-proof.md
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ cat magic-proof.md
Theorem: Some magic is happening here.
Proof: Fire magic is the best magic.
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git commit -m
error: switch `m' requires a value
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git commit -m "Add proof using fire magic."
[fire-magic 90b98e8] Add proof using fire magic.
 1 file changed, 1 insertion(+)
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git log --graph
* commit 90b98e846edb248e5c1b816fb78c76cf2eb20f1f (HEAD -> fire-magic)
| Author: Eiko <eikochanowo@outlook.com>
| Date:   Sun Dec 8 18:17:06 2024 +0000
|
|     Add proof using fire magic.
|
* commit ee464ad7f9d00972d4c15c0c8fff6ed92893a625 (master)
  Author: Eiko <eikochanowo@outlook.com>
  Date:   Sun Dec 8 17:56:01 2024 +0000

      Initial commit: Add magic theorem
```

Wow, we now have grown our DAG! The `fire-magic` branch has a new vertex (commit) that is a child of the `master` branch's vertex. Notice that it grows upwards (from old to new in time).

Let's switch back to the `master` branch.

```bash
git checkout master
cat magic-proof.md # Let's see the content of the file
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ cat magic-proof.md
Theorem: Some magic is happening here.
```

Cool, the content of the file is back to the original theorem. We are really jumping between different vertices in our DAG!

What happens if we make a different change? For example I want to add a corollary in the master branch, and let the fire-magic branch be used to explore the proof using fire-magic only.

```bash
echo "Corollary: Some magic is very useful." >> magic-proof.md
git add magic-proof.md
git commit -m "Add corollary to the magic theorem."
```

Now we have added a new vertex to the `master` branch. Let's see the DAG.

```bash
git log --graph --oneline --all 
# --all is used to show all branches
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git log --graph --oneline --all
* a979fa6 (HEAD -> master) Add corollary to the magic theorem.
| * 90b98e8 (fire-magic) Add proof using fire magic.
|/
* ee464ad Initial commit: Add magic theorem
```

This is really nice! See how the fire-magic branch and the master branch are diverging from the same vertex. The `fire-magic` branch is exploring the proof using fire magic, while the `master` branch is adding a corollary to the original theorem, and they can develop independently without interference!

You can jump back to the original vertex by checking out the commit hash.

```bash
git checkout ee464ad
cat magic-proof.md
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ cat magic-proof.md
Theorem: Some magic is happening here.
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git log --graph --all --oneline
* a979fa6 (master) Add corollary to the magic theorem.
| * 90b98e8 (fire-magic) Add proof using fire magic.
|/
* ee464ad (HEAD) Initial commit: Add magic theorem
```

You can see that our `HEAD` is now pointing to the original vertex.

### Merging Branches

Let's say that now the fire-magic branch is done and we want to merge it back to the master branch, unifying them back to a single vertex owo.

To do so, we first return to the master branch, and then merge the fire-magic branch into it.

```bash
git checkout master
git merge fire-magic
```

If there is no conflict, it will automatically merge the branches. For our case since we changed the second line into different things, there will be a conflict.

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git merge fire-magic
Auto-merging magic-proof.md
CONFLICT (content): Merge conflict in magic-proof.md
Automatic merge failed; fix conflicts and then commit the result.
```

`git` will identify the conflict and mark it for us, in the following format:

```
<<<<<<< HEAD
Content from the current branch.
=======
Content from the branch being merged (fire-magic).
>>>>>>> fire-magic
```

You can see this in the editor that we are having a conflict in the file:

```
Theorem: Some magic is happening here.
<<<<<<< HEAD
Corollary: Some magic is very useful.
=======
Proof: Fire magic is the best magic.
>>>>>>> fire-magic
```

And you just need to edit the file into the status you want, and remove the conflict markers. After that, you can add the file and commit the merge.

In this case, I just need the Corollary to put after the Proof, so I will adjust accordingly, then remove the conflict markers and the Proof line.

```
Theorem: Some magic is happening here.
Proof: Fire magic is the best magic.
Corollary: Some magic is very useful.
```

```bash
git add magic-proof.md
git commit -m "Merge fire-magic branch."
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git log --graph --oneline --all
*   6368dfa (HEAD -> master) Merge fire-magic branch.
|\
| * 90b98e8 (fire-magic) Add proof using fire magic.
* | a979fa6 Add corollary to the magic theorem.
|/
* ee464ad Initial commit: Add magic theorem
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git log --graph
*   commit 6368dfa96f0bccea3081c2ef8a40c252c218dfbc (HEAD -> master)
|\  Merge: a979fa6 90b98e8
| | Author: Eiko <eikochanowo@outlook.com>
| | Date:   Sun Dec 8 18:37:50 2024 +0000
| |
| |     Merge fire-magic branch.
| |
| * commit 90b98e846edb248e5c1b816fb78c76cf2eb20f1f (fire-magic)
| | Author: Eiko <eikochanowo@outlook.com>
| | Date:   Sun Dec 8 18:17:06 2024 +0000
| |
| |     Add proof using fire magic.
| |
* | commit a979fa63223c8524bb1e1210b20957dead0479a0
|/  Author: Eiko <eikochanowo@outlook.com>
|   Date:   Sun Dec 8 18:24:28 2024 +0000
|
|       Add corollary to the magic theorem.
|
* commit ee464ad7f9d00972d4c15c0c8fff6ed92893a625
  Author: Eiko <eikochanowo@outlook.com>
  Date:   Sun Dec 8 17:56:01 2024 +0000

      Initial commit: Add magic theorem
```

Wow! How cool is that! We have merged the branches back into a single vertex, and the DAG is now a single line again.

### Rebasing A Branch: Time-space Reordering!

Rebase allows you to change the base of a branch by 'sliding' the commits to a new base commit. Think of it as extracting the `transformation` from some base to the current point, and apply the transformation to another vertex.

Let's add a `ice-magic` branch that develops a proof using ice magic.

```bash
git checkout -b ice-magic
nvim magic-proof.md  # add a proof using ice magic here in my favorite editor
```

I add a proof using ice magic in the file, then add and commit it.

```
Theorem: Some magic is happening here.
Proof: Fire magic is the best magic.
Proof 2: Ice magic is the best magic.
Corollary: Some magic is very useful.
```

```bash
git add magic-proof.md
git commit -m "Add proof using ice magic."
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git log --graph --all --oneline
* 50a1c8c (HEAD -> ice-magic) Add proof using ice magic.
*   6368dfa (master) Merge fire-magic branch.
|\
| * 90b98e8 (fire-magic) Add proof using fire magic.
* | a979fa6 Add corollary to the magic theorem.
|/
* ee464ad Initial commit: Add magic theorem
```

Now let's say on master branch there is also some parallel development on new corollaries.

```
git checkout master
nvim magic-proof.md  # add some new corollaries here
```

```
Theorem: Some magic is happening here.
Proof: Fire magic is the best magic.
Corollary: Some magic is very useful.
Corollary 2: Some magic is very dangerous.
```

```bash
git add magic-proof.md
git commit -m "Explain the danger of Some magic"
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git log --graph --all --oneline
* 21de518 (HEAD -> master) Explain the danger of Some magic
| * 50a1c8c (ice-magic) Add proof using ice magic.
|/
*   6368dfa Merge fire-magic branch.
|\
| * 90b98e8 (fire-magic) Add proof using fire magic.
* | a979fa6 Add corollary to the magic theorem.
|/
* ee464ad Initial commit: Add magic theorem
```

We can see the diverging development very clearly. Of course we can merge these branches, but let's experiment how to use `rebase` to 'slide' the ice-magic branch, so that it starts from the latest commit on the master branch instead of `6368dfa`.

```bash
git checkout ice-magic
git rebase master
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git checkout ice-magic
Switched to branch 'ice-magic'
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git rebase master
Successfully rebased and updated refs/heads/ice-magic.
```

```
[eiko@EikoMagic14 ~/LocalDocuments/git-dag]$ git log --graph --all --oneline
* 9c31252 (HEAD -> ice-magic) Add proof using ice magic.
* 21de518 (master) Explain the danger of Some magic
*   6368dfa Merge fire-magic branch.
|\
| * 90b98e8 (fire-magic) Add proof using fire magic.
* | a979fa6 Add corollary to the magic theorem.
|/
* ee464ad Initial commit: Add magic theorem
```

Wow! Now the ice-magic are rebased on top of the latest commit on the master branch! This is really cool! You can see that the `ice-magic` branch is now a child of the latest commit on the `master` branch.

### Summary

* Git is a DAG! You can see the vertices and edges in the DAG using `git log --graph --all`. `--oneline` can simplify the output and `--all` can show all branches.

* You can create a new branch using `git checkout -b new-branch-name`.

* You can switch between branches using `git checkout branch-name`.

* Always use `git status` to see the current status of your repository owo.

* You can track and add a file to the staging area using `git add file-name`.
  
  Alternative quick / convenient options are available:

  - `git add .` to add all changes in the current directory. But this might not be what you want if you don't want to add all changes or track all files.

  - `git add -p` to interactively add changes in the file. This is useful since you can view all the changes, and you might want to add only some parts of the changes in a file.

  - `git add file1 file2 directory1 directory2` to add multiple files and directories at once.

* You can commit the changes added using `git commit -m "Commit message"`.

  This will create a new vertex in the DAG representing the current state of the repository.

* You can merge branches into current branch using `git merge branch-name`.

  If there is a conflict, you need to resolve it manually, then add and commit the file.

* You can rebase a branch using `git rebase B`

  This will 'slide' the commits in the current branch on top of the commit in the target branch `B`.

* Additional tool: 

  - try `git reflog` to see the history of your HEAD movements. This is you `travel log` in the DAG >w< ! I'm sure all wizards will need this!

  - try `gitk --all` to see the DAG in a graphical interface. This is a GUI tool that can help you visualize the DAG owo.
  
* Removing bad commits (these can be useful if you accidentally commit something you don't want, but please don't use them if you have already pushed the commits to a remote repository):

  - If you want to remove the last commit, you can use `git reset HEAD~1`. This will remove the last commit while keep the changes in the working directory.

  - If you want to remove the last commit and the changes, you can use `git reset --hard HEAD~1`. This will remove the last commit and **discard** the changes in the working directory.
