---
tags: cheatsheet
---
## stash
###  save
- save current working files
- stash with no message
```
git stash
```
- stash with a message
```
git stash save "today is the most beautiful day"
```
- stash with untracked files included
```
git stash save -u
or
git stash save --include-untracked
```
### list
- show stash list
```
git stash list
```
### apply
- apply the newest stash to current working space
```
git stash apply
```
- apply the stash with id to current working space
```
git stash apply stash@{1}
```
### pop
- apply the newest stash to current working space and delete that stash
```
git stash pop
```
- apply the stash with id to current working space and delete that stash
```
git stash pop stash@{1}
```
### show
- show short diff in the newest stash
```
git stash show
```
- show full diff in the newest stash
```
git stash show -p
```
- show diff with specific stash
```
git stash show stash@{1}
```
### branch
- create a new branch with the newest stash applied and delete that stash also
```
git stash branch another-brach-name
```
- create a new branch with a specific stash applied and delete that stash also
```
git stash branch another-branch-name stash@{1}
```
### drop
- delete the newest stash
```
git stash drop
```
- delete a stash with id
```
git stash drop stash@{1}
```
### clear
- delete the whole stash list
```
git stash clear
```
## log
- search grep in git log
```
git log --oneline grep '<text>'
```
