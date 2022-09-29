[[git]]

# How-to

## Audit git repository space usage
Find large files in a git repository's history!

```bash
git rev-list --objects --all | \
  git cat-file --batch-check='%(objectname) %(objecttype) %(objectsize) %(rest)' | \
  sort -nr -k 3 | \
  perl -ne 'm#^(\w+) blob (\d+) (.+)# or next; print "$1\t$2\t$3\n";' | \
  head -n 200 | \
  column -t -s $'\t'
```