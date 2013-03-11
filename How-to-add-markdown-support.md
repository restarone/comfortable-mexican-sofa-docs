You can add markdown support pretty easily though. Just create a tag class to handle it [see existing tags as a reference](https://github.com/comfy/comfortable-mexican-sofa/tree/master/lib/comfortable_mexican_sofa/tags):

**NOTE:** As of 1.7.0 markdown is supported out of the box. 

```ruby
require 'redcarpet'

class ComfortableMexicanSofa::Tag::PageMarkdown
  include ComfortableMexicanSofa::Tag

  def self.regex_tag_signature(identifier = nil)
    identifier ||= IDENTIFIER_REGEX
    /\{\{\s*cms:page:(#{identifier}):markdown\s*\}\}/
  end

  def content
    block.content
  end

  def render
    Redcarpet.new(content).to_html
  end

end

```

You also need to inject a helper to render the markdown.  Put the following after the above class in the same file (e.g. config/initializers/markdown_tag.rb):

```
# v1.7.1+
ComfortableMexicanSofa::FormBuilder.class_eval %Q^
  def page_markdown(tag, index)
    default_tag_field(tag, index, :text_area_tag, :data => {:cm_mode => 'text/x-markdown'})
  end
^
```

```
# v1.6.26
ComfortableMexicanSofa::FormBuilder.class_eval %Q^
  def page_markdown(tag, index)
    default_tag_field(tag, index, :method => :text_area_tag)
  end
^
```

Bam! Now you can define tags as such: {{cms:page:something:markdown}}