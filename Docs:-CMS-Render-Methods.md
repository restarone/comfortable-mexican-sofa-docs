# View Rendering

ComfortableMexicanSofa extends functionality of the `render` method to allow
rendering of CMS pages, just like regular templates. When you have
helpers/partials in place to handle instance variables set in the controller,
this is incredibly powerful feature.

To **explicitly** specify what CMS Page needs to be rendered:

```ruby
class EntriesController < ApplicationController
  def index
    @entries = Entry.all
    render cms_page: '/entries'
  end
end
```

You can also render CMS Page **implicitly**. If Rails cannot find a template
and throws *ActionView::MissingTemplate* Sofa will attempt to serve a page that
matches the request URL. For example, if /entries is routed to
*EntriesController#index* we can do this:


```ruby
class EntriesController < ApplicationController
  def index
    @entries = Entry.all
  end
end
```

If there's no *index.html.erb* Sofa will automatically render page with
full_path */entries*

You may also render CMS Layout and pass fragment content directly.

```ruby
class EntriesController < ApplicationController
  def index
    render cms_layout: "layout_identifier", cms_fragments: {
      fragment_identifier_a: 'content text',
      fragment_identifier_b: {template: 'path/to/template' },
      fragment_identifier_c: {partial:  'path/to/partial' }
    }
  end
end
```

Take a look at [ComfortableMexicanSofa::RenderMethods](//github.com/comfy/comfortable-mexican-sofa/blob/master/lib/comfortable_mexican_sofa/render_methods.rb)
module too see what's going on.
