ComfortableMexicanSofa is a plugin, so it allows you to easily access content it manages. Here's some things you can do.

You can use your existing application layout. When creating CMS layouts there's an option to use an application layout. Suddenly all CMS pages using that layout will be rendered through <%= yield %> of your application layout.

You can use CMS pages as regular views:
    
    def show
      @dinosaur = Dinosaur.find(params[:id])
      # CMS page probably should have either helper or partial tag to display @dinosaur details
      render :cms_page => '/dinosaur
    end
    
Actually, you don't need to explicitly render a CMS page like that. Sofa will try to rescue a TemplateNotFound by providing a matching CMS page.

You can access **Page** or **Field** tag content directly from your application (layouts/helpers/partials) via `cms_page_content` method. This is how you can pull things like meta tags into your application layout.
    
    # if @cms_page is available (meaning Sofa is doing the rendering)
    cms_page_content(:page_or_field_label)
    
    # anywhere else
    cms_page_content(:page_or_field_label, CmsPage.find_by_slug(...))
    
Similarly you can access **Snippet** content:
    
    cms_snippet_content(:snippet_slug)
    
You can also directly access `@cms_site`, `@cms_layout` and `@cms_page` objects from helpers, partials and application layouts used in rendering of a CMS page.