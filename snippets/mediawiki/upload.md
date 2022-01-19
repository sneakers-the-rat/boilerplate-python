## Fixing Microsoft MIME type mismatch
[Reference](https://www.mediawiki.org/wiki/Manual_talk:MIME_type_detection)

If you get `File extension ".pptx" does not match the detected MIME type of the file (application/zip).`

Edit `mediawiki/includes/mime.types`
like
```
application/zip zip jar xpi  sxc stc  sxd std   sxi sti   sxm stm   sxw stw  doc docx ppt pptx
```
