On MacOS you might see errors when uploading .svg files. It's very likely that
ImageMagick doesn't know how to handle them. To fix that try doing the following:

```
brew remove imagemagick
brew install imagemagick --with-librsvg
```