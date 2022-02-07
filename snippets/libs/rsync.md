## Use a specific [[RSA]] key when using rsync

```bash
rsync -av --progress --rsh="ssh -p <PORT> -i <ID_LOCATION>" USER@SERVER:SOURCE_PATH DEST
```
