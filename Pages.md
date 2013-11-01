Pages are exactly what you think they are: pages. A page is defined by a slug and its relationship to the parent page. So a page with slug "overview" whose parent has the slug "help" will have the full path /help/overview.

The first page you create is the homepage, and therefore you cannot specify a slug.  By default, you should be able to access the homepage without specifying your root route.  However, if you or a gem you are using need access to the `root_path` helper, specify `root :to => "cms/content#render_html"` in your routes.

Content of the page is controlled by a layout. If you have multiple layouts, selecting one from the select menu will refresh the form with fields that are available for content population.

Pages have a simple publishing control. A checkbox controls if a given page is visible to the public or if it's still a draft.