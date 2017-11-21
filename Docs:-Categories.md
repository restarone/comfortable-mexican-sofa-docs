## Overview

Pages, Snippets and Files can be categorized. It allows for easier organization
and also allows easier access to from your application.

For example, on the homepage we have some sort of a carousel element with a
number of slides that client wants to manage. However, that client doesn't have
experience with HTML, so we going to use Snippets to solve this problem. All we
need to do is assign snippets to category `carousel` and then from your
application we can easily access them like so:

```haml
  - Comfy::Cms::Snippet.for_category('carousel').each do |slide|
    .slide= slide.content
```

If you have multiple sites going on you'll need to make sure that you're not pulling content from a wrong site:

```haml
- @cms_site.snippets.for_category('carousel')
```

### Using CMS Categories on your own models

If you wish to use this functionality for your own models all you need to do is include `cms_is_categorized` in your model. Like this:

```ruby
class YourCustomModel < ActiveRecord::Base
  cms_is_categorized
  # ... more stuff
end
```

To create new categories add this line in /app/views/admin/your_model_name/index.html.haml

```haml
= render "comfy/admin/cms/categories/index", type: "YourCustomModel"
```

To assign new categories for your object add this line on template with form:

```haml
= render 'comfy/admin/cms/categories/form', form: form
```
