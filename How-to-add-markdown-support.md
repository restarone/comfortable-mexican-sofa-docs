You can add markdown support pretty easily though. Just create a tag class to handle it [see existing tags as a reference](https://github.com/comfy/comfortable-mexican-sofa/tree/master/lib/comfortable_mexican_sofa/tags): 

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

Bam! Now you can define tags as such: {{cms:page:something:markdown}}
