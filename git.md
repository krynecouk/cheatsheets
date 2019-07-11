## Ahead/behind
### local
```git
git rev-list --left-right --count master...test-branch
```
### remote
```git
git rev-list --left-right --count origin/master...origin/test-branch
```
