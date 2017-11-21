## Overview

Pages are exactly what you think they are: pages. A page is defined by a slug
and its relationship to the parent page. So a page with slug "overview" whose
parent has the slug "help" will have the full path of `/help/overview`.

The first page you create is the homepage, and therefore you cannot specify
a slug. By default, you should be able to access the homepage without specifying
your root route.  However, if you or a gem you are using need access to the
`root_path` helper, specify `root to: "comfy/cms/content#show"` in your routes.

Content of the page is controlled by a layout. If you have multiple layouts,
selecting one from the select menu will refresh the form with fields that are
available for content population.

Pages have a simple publishing control. A checkbox controls if a given page is
visible to the public or if it's still a draft.

Pages have *Redirect to Page* options. It does what it says. When hitting page
that has redirect defined it CMS with do a 302 redirect to that page.
