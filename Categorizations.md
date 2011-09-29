Pages, Snippets and Files can be categorized. It allows for easier organization and also allows easier access to from your application.

For example, on the homepage we have some sort of a carousel element with a number of slides that client wants to manage. However, that client doesn't have experience with HTML, so we going to use Snippets to solve this problem. All we need to do is assign snippets to category `carousel` and then from your application we can easily access them like so:

    - Cms::Snippet.for_category('carousel').each do |slide|
      .slide= slide.content

If you have multiple sites going on you'll need to make sure that you're not pulling content from a wrong site:

    - @cms_site.snippets.for_category('carousel')

### Using CMS Categories on your own models
If you wish to use this functionality for your own models all you need to do is include `cms_is_categorized` in your model. Like this:

    class Event < ActiveRecord::Base
      cms_is_categorized
      # ... more stuff
    end

Then all you need to do is add the form partial in the view like this:
  
    = cms_form_for @event do |form|
      = form.text_field :title
      = render :partial => 'cms_admin/categories/form', :object => form
      = form.submit 'Save'

### Automatic Categorization
Files that are uploaded via the side widget when managing layouts, pages or snippets can be automatically categorized. For that you need to enable this config in the initializer: `config.auto_file_categorization = true`. For example if we are editing a page with full path `/about-us/our-people` all files uploaded for that page will be attached to category with label `[page] /about-us/our-people`. Then you can easily use that category to display all files associated with that page.