## Get [[git]] hash within [[LaTeX]] document
- Make a `post-commit` hook in the `./git/hooks` directory like this:
```bash
#!/bin/sh
git rev-parse --short HEAD > wherever/u/want/git-version.tex
```
- Make it executable with [[chmod]]
