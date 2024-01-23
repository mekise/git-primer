# git-primer

> :warning: Run the all the following in the terminal (Linux or Mac) or Git Bash (Windows) unless specified otherwise!

## Preliminary
Make sure you have Git installed. On Linux and Mac, just open the terminal and run `git --version`. This should give you the version you have installed. On Windows check if you have the application `Git bash`. If not, install Git from this link https://git-scm.com/download/win

## Getting started
If you want a general understanding of Git, follow https://git-scm.com/book/en/v2 or https://docs.github.com/en/get-started/getting-started-with-git

## Set up SSH
This might be a tricky one, every step and word counts. Follow this guide, **word-by-word** https://docs.github.com/en/authentication/connecting-to-github-with-ssh

## Git cheatsheet
- https://training.github.com/downloads/github-git-cheat-sheet/
- https://education.github.com/git-cheat-sheet-education.pdf
- https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet

## GitHub workflow
Later, we will talk about working on remotes using GitHub. When collaborating, there is an important workflow that we must adopt. The GitHub philosophy of workflow is quite simple, you find it here https://docs.github.com/en/get-started/quickstart/github-flow

As a recap of the important steps to follow when developing a new feature are:
1. Create a branch for a new feature
2. Work on the feature
3. Open pull request to merge (resolving conflicts)
4. Close the merged branch

> [!NOTE]
> Have simple tests in place to be sure everything always works in the main branch

## Config setup
Configure name and email.
```
git config --list
git config --global user.name 'Name Surname'
git config --global user.email 'user@email.com'
```

## Change your main editor
This will be the editor Git will open by default.
```
git config --global core.editor "vim"
git config --global core.editor "'C:/Program Files (x86)/sublime text 3/subl.exe' -w"
git config --global core.editor "code --wait"
```

## Basic commands - local changes
Let's see how to create a new local project and work on it tracking it with Git.
```
touch file1.jl (create a file)
git init
git add file1.jl
git status
git restore --staged file1.jl
git add .
git add *.jl
git commit
git commit -m 'Add file1'
git branch (list local branches)(option -r to check remote branches)
git branch feature1
git checkout feature1 (run `git chekout -b feature1` to create the branch and immediately move into it without the need to run the previous line)
```
Now, make some changes in the branch feature1 (e.g. `echo "some change" >> file1.jl ; cat file1.jl`)

> [!IMPORTANT]  
> Once you finished working on the feature, you need to add it and commit it to the branch. If you checkout to a different branch before committing, all the uncommitted work you have done will be carried over to the branch you are now in.

To merge, go to the main branch:
```
git checkout main
git merge feature1
``` 
This kept the main branch safe until the new feature was polished. Now, we have the new feature in the main branch as well.

Once merged, you can should delete the branch to avoid accidental use.
```
git branch -d feature1
```

> [!IMPORTANT]  
> When we start working with a remote, we will need to close the online branch as well. You can do this running `git push origin -d feature1`.

## Resolve a conflict
You will find conflicts while merging with other people's work. Sometimes, you will even find conflicts when merging your own code. Let's resolve a conflict.

When merging, this is the type of message that you will see
```
> git merge feature1
Auto-merging file1.jl
CONFLICT (content): Merge conflict in file1.jl
Automatic merge failed; fix conflicts and then commit the result.
```
Performing a `git status` we obtain
```
> git status
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   file1.jl

no changes added to commit (use "git add" and/or "git commit -a")
```
As suggested, we must fix the conflict in `file1.jl` and commit.
```
<<<<<<< HEAD
some line in main
=======
some other line in feature1
>>>>>>> feature1
```
`<<<<<<< HEAD` indicates the version of the branch we are in. `=======` is a delimiter. `>>>>>>> feature1` indicates the version of the branch we are trying to merge.

Resolve the conflict by deleting all this text and adding the lines you want, for example:
```
some other line in feature1
```
Now, run `git add file1.jl` and `git commit -m "Fix merge conflict"` and all should be good!

## Working with a remote
All we have done until now was **local**, let's add a remote. To put these files online create an empty repo GitHub, then:
```
git remote (to check if there is any remote; there should be none. -v verbose)
git remote add origin git@github.com:USERNAME/REPONAME.git
git push -u origin main
``` 
From now on, you can use pull and push to communicate with the remote:
```
git status
git pull (= git fetch; git merge)
```
Make some changes, then:
```
git add .
git commit -m "Add this change"
git push
```

Here, some commands to work with the branches on the remote
```
git branch -r (to list the branches on the remote)
git push -u origin feature1 (to push a new branch on the remote)
git push -d origin feature1 (to close a branch on the remote)
```

## The life-saver .gitignore
```
touch .gitignore
```
Add some entries e.g. directories, extensions, etc.
```
/directory
*.txt
```

## Stashing
```
git stash push -m "Some change here and there" (or simply git stash)
git stash apply # (where # is the index)
git stash list
git stash drop #
git stash pop #
git stash clear
```

## Other commands
> [!NOTE]
> `HEAD` is like a local pointer to the last commit of the current branch
```
git clone git@github.com:USERNAME/REPONAME.git (if the repo is online and you need to work on it)
git log (--graph)
git rebase (HEAD, ~, etc.)
git reset HEAD~1 (~1 1 behind, ~2 2 behind etc.) (default to --mixed, alternatives: --soft lose commit but NOT changes, --hard lose commit AND changes)
git remote (list all the remote names)
```
