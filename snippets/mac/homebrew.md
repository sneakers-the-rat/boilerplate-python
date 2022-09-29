## Install an Old Version
When the `papckage@version` syntax isn't supported
https://stackoverflow.com/a/64125796/13113166

```bash
TAP=...     # <org>/<repo>, for example "my-org/homebrew-old"
MODULE=...  # name of module you want to install, e.g. "hugo"
VERS=...    # version of $MODULE you want to install, e.g., "0.80.0"
brew tap-new $TAP
brew extract --version $VERS $MODULE $TAP
brew install $TAP/$MODULE@$VERS
```
