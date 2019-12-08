On MacOS you might see errors when uploading .svg files. It's very likely that
ImageMagick doesn't know how to handle them. To fix that try doing the following:

```
brew remove imagemagick
brew install imagemagick --with-librsvg
```

Note newest `brew` removed options for some reason, but you can install older version:
`brew install https://github.com/Homebrew/homebrew-core/raw/46a2ef7c9f0380b8e19f8dfe37270caa27581353/Formula/imagemagick.rb --with-librsvg`

Or use MacPorts.
