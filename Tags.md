There are a number of cms tags that define where the content goes and how it's populated. **Page**, **Field**, **Collection** and **PageFiles** tags are used during layout creation. **Snippet**, **Helper** and **Partial** tags can be peppered pretty much anywhere. Tag is structured like so:
    
    {{ cms:page:content:text }}
        \    \     \      \ 
         \    \     \      ‾ tag format or extra attributes
          \    \     ‾‾‾‾‾‾‾ label/slug/path for the tag, 
           \    ‾‾‾‾‾‾‾‾‾‾‾‾ tag type (page, field, snippet, helper, partial)
            ‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾ cms tag identifier
           
## Page
Page tags are pieces of text content that will get rendered on the page. Format defines how form field gets rendered in the page editing/creation section of the admin area.
    
    {{ cms:page:some_label:text }}
    {{ cms:page:some_label }}             # shorthand for above. 'text' is default format for pages
    {{ cms:page:some_label:string }}      # in admin area text field is displayed instead of textarea
    {{ cms:page:some_label:datetime }}    # similarly, datetime widget in the admin area
    {{ cms:page:some_label:integer }}     # a number field
    {{ cms:page:some_label:rich_text }}   # wymiwyg editor will be used to edit this content
    
## Field
Field tags are pieces of text content that are **NOT** rendered on the page. They can be accessed in your application's layout / helpers / partials via `cms_page_content(:some_label)` helper method. Useful for populating things like `<meta>` tags.
    
    {{ cms:field:some_label:string }}
    {{ cms:field:some_label }}             # same as above. 'string' is default format for fields
    {{ cms:field:some_label:text }}        # in admin area text field is displayed instead of textarea
    {{ cms:field:some_label:datetime }}    # similarly, datetime widget in the admin area
    {{ cms:field:some_label:integer }}     # a number field
    
## Snippet
Snippet tags are bits or reusable content that can be used anywhere. Imagine creating content like a sharing widget, or business address that you want to randomly use across your site.
    
    {{ cms:snippet:some_label }}
    
## Helper
Helper is a wrapper for your regular helpers. Normally you cannot have IRB in CMS content, so there are tags that allow calling helpers and partials.
    
    {{ cms:helper:method_name }}          # same as <%= method_name() %>
    {{ cms:helper:method_name:x:y:z }}    # same as <%= method_name('x', 'y', 'z') %>
    
## Partial
Partial tags are wrappers just like above helper ones.
    
    {{ cms:partial:path/to/partial }}     # same as <%= render :partial => 'path/to/partial' %>
    {{ cms:partial:path/to/partial:a:b }} # same as <%= render :partial => 'path/to/partial',
                                          #   :locals => { :param_1 => 'a', :param_1 => 'b' } %>
                                          
## File
Uploaded files can be linked using these tags:

    {{ cms:file:file_name.ext }}              # File URL: /system/files/123/file_name.ext
    {{ cms:file:file_name.ext:link }}         # Link tag: <a href='file_url'>file_label</a>
    {{ cms:file:file_name.ext:link:label }}   # Link tag with label: <a href='file_url'>label</a>
    {{ cms:file:file_name.ext:image }}        # Image tag: <img src='file_url' alt='file_label' />
    {{ cms:file:file_name.ext:image:label }}  # Image tag with label: <img src='file_url' alt='label' />
    
## Asset
You can define CSS and Javascript in your CMS Layouts. This is how you can easily pull it in:

    {{ cms:asset:layout_slug:css }}           # URL for CSS: /cms-css/site_id/layout_slug.css
    {{ cms:asset:layout_slug:css:html_tag }}  # Link tag: <a href='css_url' />
    {{ cms:asset:layout_slug:js }}            # URL for JS: /cms-js/site_id/layout_slug.js
    {{ cms:asset:layout_slug:js:html_tag }}   # Script tag: <script src='js_url'></script>

## Collection
Collection is just a smarter, more user-friendly Partial tag. Collection automatically generates a partial tag for an object selected during page creation/editing.
This a tag that you generally want to use on the Layout level, as it's not going to do anything anywhere else. Here's a signature of the Collection tag:
    
    {{ cms:collection:some_label:collection_class:collection_partial:collection_title:collection_identifier:collection_params }}
    
Looks a bit complicated so let's deconstruct it:

    collection_class      -> Class name of the object that you want to render.
                             If it's something like Herp::HerpityDerp then the value should be: `herp/herpity_derp`
    collection_partial    -> (optional) Based on the above will default to: `partials/herp/herpity_derps`
    collection_title      -> (optional) In the admin form what method identifies the object? Defaults to `label`
    collection_identifier -> (optional) What we are storing to identify object. Defaults to `id`
    collection_params     -> (optional) Like for the Partial you can pass extra params that will be used to render the tag
    
What if don't want to list all objects in the admin? You can define a scope called `cms_collection` that takes arguments from the `collection_params`. Observe:
    
    class Herp::HerpityDerp < ActiveRecord::Base
      scope cms_collection, lambda{|*args| where(:color => args[0], :smell => args[1])}
    end

## PageFile and PageFiles
This tag allows you to attach files directly to the page and render them out. Let's assume that we have an image tag on the Layout and it's source needs to be populated via file that is uploaded for some page. All you need to do is add this tag in place of the `src` content:
    
    {{ cms:page_file:header }}
    
This will output the URL of the uploaded file. There are other variations of this tag:
    
    {{ cms:page_file:header:url }}          # File URL: /system/files/123/file_name.ext
    {{ cms:page_file:header:link }}         # Link tag: <a href='file_url'>file_label</a>
    {{ cms:page_file:header:link:label }}   # Link tag with label: <a href='file_url'>label</a>
    {{ cms:page_file:header:image }}        # Image tag: <img src='file_url' alt='file_label' />
    {{ cms:page_file:header:image:label }}  # Image tag with label: <img src='file_url' alt='label' />
    {{ cms:page_file:header:field }}        # Won't render anything out. Access via cms_page_content helper
    
The most useful way to render this tag is via a partial:
    
    {{ cms:page_file:header:partial }}                      # with default path to 'partials/page_file'
    {{ cms:page_file:header:partial:path/to/partial }}      # with defined path
    {{ cms:page_file:header:partial:path/to/partial:a:b }}  # with params 'a' and 'b'. See partial tag
    
If you need to handle multiple files at the same time you need to use PageFiles tag. Everything else is pretty much the same as for the single file.
    
    {{ cms:page_files:header }}

When using to upload images you can actually automatically resize/crop them. See the available [resize/crop options](http://www.imagemagick.org/Usage/resize/#resize).

    {{ cms:page_file:header:image[50x50#]:label }}
    {{ cms:page_files:photos:partial[100x50>]:path/to/partial }}
    