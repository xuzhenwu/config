# Git

## Cheat Sheet

```
# commonly used 
git init <directory>
git status
git add --all
git commit -am "<message>"
git remote add <name> <url>
git remote -v
git push <remote> <branch>
git pull <remote> <branch>
git cheakout <branch>
git merge <branch>
git diff <branch1> <branch2> <file>

# be cautious using this 
git push <remote> --force
git push <remote> --all
```

To have more information, you can access a cheat sheet via https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet

## global setting

you can access the git setting by the following script, define username, email, and proxy

``` git config --global --edit  
git config --global --edit  
```

```
[user]
        name = xuzhenwu
        email = xuzhw5@mail2.sysu.edu.cn
[filter "lfs"]
        clean = git-lfs clean -- %f
        smudge = git-lfs smudge -- %f
        process = git-lfs filter-process
        required = true
[gui]
        recentrepo = C:/Users/Administrator/source/repos/xuzhenwu
[http]
        cookiefile = C:\\Users\\Administrator\\.gitcookies
        proxy = http://127.0.0.1:10809
[https]
        proxy = http://127.0.0.1:10809/
```



