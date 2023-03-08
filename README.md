# Git_Practice

Even though I start using git when I born, I could never master the git whne I die. :-(

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