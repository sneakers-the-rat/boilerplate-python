## Scraping sites recursively

```bash
#!/bin/bash
wget \
  --no-clobber \       # don't overwrite files you already have
  --convert-links \    # Fix absolute links to work locally
  --random-wait \      # Wait between each request 
  --progress=bar  \
  --recursive \        # Scrape recursively!
  --level=0 \          # Scrape n pages deep (0=infinite)
  --adjust-extension \ # fix weird extension names
  -A "pdf,csv,xls,xlsx,doc,docx,txt" \ # limit filetypes
  -p \                 # get all files linked in page (images, etc.)
  -e robots=off \
  https://yoururl.com # the base url to start
```

Other options:
- `-R` Give a pattern of urls to reject, like `"*index.html,*search*"` (using globs)
- `-H` Span hosts, or download files from different domain than host