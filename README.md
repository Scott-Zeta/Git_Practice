# Git_Practice

Even though I start using git when I born, I could never master the git when I die. :-(

## Git configuration
1. System: store in /etc/gitconfig or Git in program files(windows)
    git config --system
2. User: ~/.gitconfig or user/yourUserName/.gitconfig
    git config --global
3. Porjec: project/.git/config
    git config

user ```git config --list``` to check all the configuration
What should I config first?
1. user.name
2. user.email
3. color.ui true (like syntax)

## Read a git log
```git log```
commit eb3d2f9dafd3e52188546acdc216000a7e4bb0af (HEAD -> main, origin/main, origin/HEAD)
Author: Scott-Zeta <wc070211@gmail.com>
Date:   Tue Mar 7 18:58:57 2023 +1030

    Let's try to write a long summary
    Let's try to write a long summary

```git log -n 5```
show me the most recent 5 commit

```git log --since=2023-01-01```
```git log --until=2023-01-01```
show me the commit in certain time period

```git log --author="Scott"```
show me commit by author(no need full name)

```git log --grep="Bugfix:"```
--grep for global regular expression, search for any commit include the "Bugfix"
This is why need to write a standard commit message

You can chain these command up together like:
```git log --since=2022-03-01 --until=2023-03-01 --author=="scott" --greo="initial"``` 
You can chain these command up together like:
```git log --since=2022-03-01 --until=2023-03-01 --author=="scott" --greo="initial"``` 

## Three tree in Git (Format might be messy in reading mode :-<)
1. Working
 ||    ```git checkout -- <file>``` discard/undo the change when it is still in working layer 
 ||    ```git diff``` compare difference in working tree 
\  /   ```git add/rm/mv``` put it on "track"
 \/    ```git clean -n/-f``` remove the untracked file(Junk, temporary) !will be remove forever!
2. Staging index
 ||    ```git reset HEAD <file>``` to unstage\undo the change when in stage layer 
 ||    ```git diff --staged``` only compare in Staging tree
\  /   ```git commit```
 \/    ```git commit -a``` will skip staging!
3. Repository
```git log``` is in this layer, Is nothing in Working and Staging index, it would say "working tree is clean"
```git show checksum``` will show the change in specific commit
```git diff checksum1...checksum2/HEAD``` compare difference between two commit
```git commit --amend -m "add a new change in previous commit"``` Opps, I want to add more but don't want to make a new commit.
```git checkout checksum -- <file>``` retreat to old version commit, it will be put in the staging layer
```git revert checksum``` revert to olde version, it will be put in the Repository layer

## HEAD
A pointer varible that point to the current branch in repository, usually latest version of current branch.

## GitIgnore
useful resouce: https://github.com/github/gitignore
```git rm --cached <fileName>``` stop tracking some files after add it into .gitignore
Can be complex to remove previous change history(If you accidently upload your password,key ```:-(``` )

## Tree-ish
Use checksum(SHA-1) to refer to a commit, ```^```refer for its parent commit(one before, ```^^``` for two or ```~2```)

## Branch
```git branch <newBranchName>``` Current branch will be marked as green.
```git checkout <branchName>``` switch to branch
!!! Can not switch with Uncommited changes with conflict, what you should do?
1. commit
2. discard
3. stash?
```git diff <branch_name1>..<branch_name2>``` for compare two branches, can use combine with ```^``` for older version
You can not delete branch you are in, and will get warning if there are something not mergeed by checking ```branch --no-merged```

## Reset
1. Soft: Move HEAD pointer, does not change staging index, does not change working directory ```git reset --soft <tree-ish>```, similar to ```--ammed``` roll all change back to staging index, useful if you want to combine several commit
2. Mixed: ```git reset --mixed <tree-ish>``` roll back to working directory, usefule when you want to seperate the commit
3. Hard: ```git reset --hard <tree-ish>``` discard everything, pretend nothing hanppend. Usually for undo the merge

## Merge
how to reduce merge conflit?
1. keep lines short
2. keep commits small and focused
3. beware edit the whitespace
4. merge often, less conflict
5. merge from master to brach (let people who charge the branch handle it)

## Stash
An isolated fourth area from the Three main layer.
Stash a change before switch branches by ```git stash save <stashName>```, Stash won't save with untracked file by default, check it by ```git stash list```
(Theorotically, it saved a snapshot of change, then you can use it in anywhere)
```git stash pop``` pop up a change directly and remove it from the stash, ```appply``` make the change but keep it. (Like pop and peek)
```git stash drop stash@{list number}``` abort the change inside the stash

## Remote
```git remote add origin <GitHub url>```, config the git remote settting, origin refer to the remote "name", usally only have one.
```git push -u <remote name(origin)> <branch name>``` It will ask username and password of GitHub this step
```git branch -r``` only show the remote branch
```git pull``` = ```git fetch```(check the conflict before merge) + ```git merge```