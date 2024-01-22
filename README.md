# git-primer

> :warning: Run the following lines in the terminal (Linux or Mac) or Git Bash (Windows)

## Getting started
https://docs.github.com/en/get-started/getting-started-with-git

## Set up SSH
https://docs.github.com/en/authentication/connecting-to-github-with-ssh

## GitHub workflow
https://docs.github.com/en/get-started/quickstart/github-flow

## Important concepts
1. Create a branch for a new feature
2. Work on the feature
3. Open pull request to merge (resolving conflicts)
4. Have simple tests in place to be sure everything always works in the main branch

## Config setup
Configure name and email:
```
git config --list
git config --global user.name 'Name Surname'
git config --global user.email 'user@email.com'
```

## Change your main editor (vim or Sublime suggested)
```
git config --global core.editor "vim"
git config --global core.editor "'C:/Program Files (x86)/sublime text 3/subl.exe' -w"
git config --global core.editor "code --wait"
```

## Basic commands - local changes
```
touch file1.jl
git init
git add file1.jl
git status
git rm --cached file1.jl
git add .
git add *.jl
git commit
git commit -m 'Add file1'
git branch (list local branches)(option -r to check remote branches)
git branch feature1
git checkout feature1
```

Now, make some changes in the branch feature1 (e.g. `echo "some change" >> file1.jl ; cat file1.jl`)

To merge, go to the main branch:
```
git checkout main
git merge feature1
``` 
This kept the main branch safe until the new feature was polished.

## Resolve a conflict
You will find conflicts while merging with other people's work. You will find conflicts even when merging your own code. Let's resolve a conflict.

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
As suggested, we need to fix the conflict in `file1.jl` and commit.
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

Push a new branch on the remote
```
git push -u origin feature1 (or --set-upstream)
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
