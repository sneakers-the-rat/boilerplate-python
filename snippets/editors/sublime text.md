## Autobuild latex on save
- install `hooks` package
- open syntax specific settings for latex (`LaTeX.sublime-settings`)
```json
// These settings override both User and Default settings for the LaTeX syntax
{

  "on_post_save_async_language": [
    {
        "command": "build",
        "scope": "window"
    }
  ]

}

```

## Build [[LaTeX]] using [[tectonic]] and [[LaTeXTools]]
In LaTeXTools user settings...
(Need to put the "echo" because otherwise it adds the filename to the end for some reason.)
```json
{
	"builder": "script",
	"builder_settings" : {
		"script_commands": "echo $file; tectonic -X build --open"
	}
}

```
