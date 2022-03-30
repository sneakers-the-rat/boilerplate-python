## Make a new tag
https://git-scm.com/book/en/v2/Git-Basics-Tagging

Basic annotated tag
```bash
git tag -a <tag> -m "<tag message>"
```

Tag a specific [[commit]]

```bash
git tag -a <tag> -m "<tag message>" <commit hash>
```

## Sharing Tags
Push one tag
```bash
git push <remote> <tag>
```

Push all tags
```bash
git push <remote> --tags
```

## Deleting Tags
Locally
```bash
git tag -d <tag>
```

On remotes
```bash
git push origin --delete <tag>
```

