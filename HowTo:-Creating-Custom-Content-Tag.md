Here's an example of a very simple content tag that can be inserted anywhere
to render random image of given dimentions:

Create file `/lib/cms_tags/lorem_picsum.rb`. And require it from somewhere.
`application.rb` is not a bad place.

```ruby
# Renders image tag from http://picsum.photos
# Example: {{cms:lorem_picsum 400, 300}}
class LoremPicsum < ComfortableMexicanSofa::Content::Tag

  attr_reader :path, :locals

  def initialize(context:, params: [], source: "")
    super
    @width  = params[0]
    @height = params[1]

    unless @width.present?
      raise Error, "Need at least one dimension of the image"
    end
  end

  def content
    dimensions = [@width, @height].compact.join('/')
    "<img src='https://picsum.photos/#{dimensions}'/>"
  end
end

ComfortableMexicanSofa::Content::Renderer.register_tag(
  :lorem_picsum, LoremPicsum
)
```

For inspiration, take a look at existing content tags: https://github.com/comfy/comfortable-mexican-sofa/tree/master/lib/comfortable_mexican_sofa/content/tags
