

## hash


## Remove file from git commit history
Use [git filter repo](https://github.com/newren/git-filter-repo):
```bash
git filter-repo --path file_to_delete.csv --invert-paths
```
Typically `filter-repo` only keeps the files specified, to to keep *all except* the specified file, use the `--invert-paths` flag.


