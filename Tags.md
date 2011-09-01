There are a number of cms tags that define where the content goes and how it's populated. **Page** and **Field** tags are used during layout creation. **Snippet**, **Helper** and **Partial** tags can be peppered pretty much anywhere. Tag is structured like so:
    
    {{ cms:page:content:text }}
        \    \     \      \ 
         \    \     \      ‾ tag format or extra attributes
          \    \     ‾‾‾‾‾‾‾ label/slug/path for the tag, 
           \    ‾‾‾‾‾‾‾‾‾‾‾‾ tag type (page, field, snippet, helper, partial)
            ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾ cms tag identifier
           
### Page
Page tags are pieces of text content that will get rendered on the page. Format defines how form field gets rendered in the page editing/creation section of the admin area.
    
    {{ cms:page:some_label:text }}
    {{ cms:page:some_label }}             # shorthand for above. 'text' is default format for pages
    {{ cms:page:some_label:string }}      # in admin area text field is displayed instead of textarea
    {{ cms:page:some_label:datetime }}    # similarly, datetime widget in the admin area
    {{ cms:page:some_label:integer }}     # a number field
    {{ cms:page:some_label:rich_text }}   # wymiwyg editor will be used to edit this content
    
### Field
Field tags are pieces of text content that are NOT rendered on the page. They can be accessed via your application's layout / helpers / partials etc. Useful for populating this like <meta> tags.
    
    {{ cms:field:some_label:string }}
    {{ cms:field:some_label }}            # same as above. 'string' is default format for fields
    {{ cms:page:some_label:string }}      # in admin area text field is displayed instead of textarea
    {{ cms:page:some_label:datetime }}    # similarly, datetime widget in the admin area
    {{ cms:page:some_label:integer }}     # a number field
    
### Snippet
Snippet tags are bits or reusable content that can be used anywhere. Imagine creating content like a sharing widget, or business address that you want to randomly use across your site.
    
    {{ cms:snippet:some_label }}
    
### Helper
Helper is a wrapper for your regular helpers. Normally you cannot have IRB in CMS content, so there are tags that allow calling helpers and partials.
    
    {{ cms:helper:method_name }}          # same as <%= method_name() %>
    {{ cms:helper:method_name:x:y:z }}    # same as <%= method_name('x', 'y', 'z') %>
    
### Partial
Partial tags are wrappers just like above helper ones.
    
    {{ cms:partial:path/to/partial }}     # same as <%= render :partial => 'path/to/partial' %>
    {{ cms:partial:path/to/partial:a:b }} # same as <%= render :partial => 'path/to/partial',
                                          #   :locals => { :param_1 => 'a', :param_1 => 'b' } %>