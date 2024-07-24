# base64 Shortcode For Quarto

Easily embed base64 encoded files in your Quarto documents.

Why would you want to do this? If you're using the [shinylive Quarto extension](https://quarto-ext.github.io/shinylive/), you can use the `base64` shortcode to embed binary files in your Shinylive apps. 

If you aren't using Shinylive, pandoc can help you embed images in your documents via `--embed-resources` (or `embed-resources: true` in Quarto). But this applies to all images and resources in your document. If you find yourself wanting to embed a single image or resource: the `base64-data` shortcode can help!

## Installing

```bash
quarto add gadenbuie/quarto-base64
```

This will install the extension under the `_extensions` subdirectory.
If you're using version control, you will want to check in this directory.

## Using

### base64

To encode a file into a base64 string, use the `base64` shortcode.

````{.markdown shortcodes="false"}
```{shinylive-python}
#| standalone: true
#| components: [editor, viewer]
#| layout: vertical
## file: app.py
from pathlib import Path

from shiny.express import render, ui

@render.ui
def image():
    return ui.image(src="photo.png")

## file: www/photo.png
## type: binary
{{< base64 photo.png >}}
```
````

### base64-data

To encode a file into a base64 data URI, use the `base64-data` shortcode.

````{.markdown shortcodes="false"}
![]({{< base64-data photo.png >}})
````

The `base64-data` shortcode will automatically guess [the MIME type of the file](https://www.iana.org/assignments/media-types/media-types.xhtml) using [the puremagic Lua module](https://github.com/wbond/puremagic). If it guesses wrong, or can't determine the MIME type, you can specify the MIME type explicitly.

````{.markdown shortcodes="false"}
![]({{< base64-data photo.png "image/png" >}})
````

## Example

Here is the source code for a minimal example: [example.qmd](example.qmd).
