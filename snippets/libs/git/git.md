## Make new repository from existing directory

- Create new repository on github or other vcs remote
- Create new local repository
```bash
git init
git add .
git commit -m "message"
git remote add origin https://github.com/<username>/<repo>
```
- Configure repository (or use `--global` to set for all repositories)

```shell
git config push.default simple
git config pull.rebase false
```
- Merge with remote repository and push
```shell
git fetch
git branch --set-upstream-to=origin/main
git pull --allow-unrelated-histories
git push
```


## Global .gitignore

```shell
nano ~/.gitignore
git config --global core.excludesfile ~/.gitignore
```

## Securely save credentials
[[TODO]]







