# View Helpers

You can access **Page** or **Field** tag content directly from your application (layouts/helpers/partials) via `cms_page_content` method. This is how you can pull things like meta tags into your application layout.
    
    # if @cms_page is available (meaning Sofa is doing the rendering)
    cms_page_content(:page_or_field_label)
    
    # anywhere else
    cms_page_content(:page_or_field_label, CmsPage.find_by_slug(...))
    
Similarly you can access **Snippet** content:
    
    cms_snippet_content(:snippet_slug)