[Stack Overflow question](https://stackoverflow.com/questions/1580596/how-do-i-make-git-ignore-file-mode-chmod-changes)

there is a problem when you open your git repository . all files seem to be changed and git repository shows that all files are changed but when you go for inspecting say to you that file permission is changed .

to solve that issue go to that repository's folder and run this command :

```shell
git config core.fileMode false
```