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
git config --blobal user.email 'user@email.com'
```

## Change your main editor (vim or Sublime suggested)
```
git config --global core.editor "vim"
git config --global core.editor "'C:/Program Files (x86)/sublime text 3/subl.exe' -w"
git config --global core.editor "code --wait"
```

## Basic commands
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

Now, make some changes in the branch feature1 (e.g. `"some change" >> file1.jl ; cat file1.jl`)

To merge, go to the main branch:
```
git checkout main
git merge feature1
``` 
This kept the main branch safe until the new feature was polished.

You will find conflicts while merging when working with people (even on your own). Let's resolve a conflict.

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
If the repo is already online and you need to clone it:
```
git clone git@github.com:USERNAME/REPONAME.git
```

## Push a new branch on the remote (-u is the same as --set-upstream in git)
```
git push -u origin feature1
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
git log (--graph)
git rebase (HEAD, ~, etc.)
git reset HEAD~1 (~1 1 behind, ~2 2 behind etc.) (default to --mixed, alternatives: --soft lose commit but NOT changes, --hard lose commit AND changes)
git remote (list all the remote names)
```
