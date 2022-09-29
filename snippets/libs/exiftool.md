## Scrub [[metadata]] from [[PDF]]s
also using [[qpdf]]

```bash
exiftool -q -q -all:all= <INPUT_FILE> -o <OUTPUT_FILE>
qpdf --linearize --replace-input <OUTPUT_FILE>
```

## Extract all images from PDFs
```bash
exiftool -a -b -ee -embeddedimage -W <OUTPUT_IMAGE_PREFIX>_%.3g3.%s <PDF_FILE>.pdf
```