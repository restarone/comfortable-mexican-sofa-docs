## Instance Variables
When rendering partials and helpers from CMS, you have access to `@cms_site`, `@cms_layout` and `@cms_page`. For example, you can probably use the page object to render a navigation bar. The application layout also has access to those variables if used in Cms::Layout.

## Helper methods
There are two helper methods available: `cms_block_content()` and more frequently used `cms_snippet_content()`.

`cms_block_content` is used to access content inside page blocks. If you have a page that has its content stored against `{{cms:page:content}}` or `{{cms:field:content}}` you can easily retrieve it like so: `cms_page_content(:content)`. If you want to use this method outside CMS rendering, like in your own view/controller, you need to provide a Cms::Page object: `cms_block_content(:content, Cms::Page.find_by_full_path('/herp/derp'))`

Similarly, you can get the snippet content with `cms_snippet_content(:example)` if you have a Cms::Snippet with slug 'example'. Once again, outside CMS rendering you may need to provide Cms::Site object (although it's usually found automatically): `cms_snippet_content(:example, Cms::Site.find_by_hostname('example.com'))`

In versions prior to 1.12.0 `cms_page_content()` is used instead of `cms_block_content()`.

## Render CMS Page
You can use CMS pages as regular views:

    def index
      @events = Event.all
      render :cms_page => '/events/index'
    end
  
Now a page with full_path '/events/index' will be rendered. You probably want to define a partial tag that will handle rendering of the `@events`. Like so: `{{cms:partial:events/index}}`. Generally it makes sense to have normal view files at the start, and then you just rename them to be a partial (leading underscore character).

Note that ComfortableMexicanSofa will attempt to rescue `ActionView::MissingTemplate` by serving a matching CMS page.

## Render CMS Layout
What if you don't want to create CMS pages and partials but want to render your regular Rails template inside CMS layout? You can do it like so:
    
    def index
      @events = Event.all
      render :cms_layout => 'three_column', :cms_blocks => {
        :column_a => 'Content About Events',
        :column_b => { :template => '/events/index' },
        :column_c => { :partial  => '/events/calendar' }
      }
    end
    
So if you have a layout with slug `three_column` with content like this: "`{{cms:page:column_a}} {{cms:page:column_b}} {{cms:page:column_c}}`". It should be pretty obvious that `column_a` will be populated with provided text, `column_b` will use rendered template and `column_c` will have rendered partial as its content.

If layout has a simple tag like this: "`{{cms:page:content}}`" and you're OK with rendering the actual default template for that action you can simplify render call to this:

    def index
      # same as:
      # render :cms_layout => 'one_column', :cms_blocks => { :content => { :template => '/events/index' }}
      render :cms_layout => 'one_column'
    end
    
Please note that for `render :cms_layout` instance variable `@cms_page` is not available as there's no actual page. For purposes of generating navs, etc consider either reusing one of the existing pages or instantiating a new one with attributes that you need.