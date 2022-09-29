## Make a [[torrent]] file
### [[torrenttools]]
https://github.com/fbdtemme/torrenttools

```bash
torrenttools create \
  --announce <url> \
  --piece-size <size[K|M]>
  --protocol hybrid \
  --include <regex> \
  --exclude <regex> \
  -o <filename>.torrent
  <input_files>
```

- or use `--protocol 1` if compatibility issues

### [[mktorrent]]
https://manpages.debian.org/testing/mktorrent/mktorrent.1.en.html

