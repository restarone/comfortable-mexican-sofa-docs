## Overview

All you need to know about Files is that they are handled by [ActiveStorage](https://github.com/rails/rails/tree/master/activestorage). Thus `Comfy::Cms::File`
records have `attachment` method that you can use.

Attachments against page fragments (`Comfy::Cms::Fragment`) use `attachments`
method as there might be more than one.
