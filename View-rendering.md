# View Rendering

ComfortableMexicanSofa extends functionality of the `render` method to allow rendering of CMS pages, just like regular templates. When you have helpers/partials in place to handle instance variables set in the controller, this is incredibly powerful feature.

To **explicitly** specify what CMS Page needs to be rendered:
    
    class EntriesController < ApplicationController
      def index
        @entries = Entry.all
        render :cms_page => '/entries'
      end
    end
    
You can also render CMS Page implicitly. If Rails cannot find a template and throws *ActionView::MissingTemplate* Sofa will attempt to serve a page that matches the request URL. For example, if /entries is routed to *EntriesController#index* we can do this:
    
    class EntriesController < ApplicationController
      def index
        @entries = Entry.all
      end
    end

If there's no *index.erb.html* Sofa will automatically render page with full_path */entries*