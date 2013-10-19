Sofa doesn't make assumptions about how you want to render navigation elements, so it doesn't provide you with helper methods to do so. However you have access to page objects directly and can do it yourself rather easily. Generally you would have something like this in your helper/partial:

    - @cms_site.pages.root.children.published.each do |page|
      = link_to page.label, page.full_path

Then you can use that from the application layout, or CMS layout/page via a tag.

[Zhao Lu](http://github.com/zlu): Instead of page.full_path, using page.url maybe more useful especially for a multi-site configuration.