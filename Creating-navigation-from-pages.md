Sofa doesn't make assumptions about how you want to render navigation elements, so it doesn't provide you with helper methods to do so. However you have access to page objects directly and can do it yourself rather easily. Generally you would have something like this in your helper/partial:

    - @cms_site.pages.root.children.published.each do |page|
      = link_to page.label, page.full_path

Then you can use that from the application layout, or CMS layout/page via a tag.

[Zhao Lu](http://github.com/zlu): Instead of page.full_path, using page.url maybe more useful especially for a multi-site configuration.

For those not using haml, something like this can be used:

      <% @cms_page.children.published.each do |p| %>
        <%= link_to p.label, p.url(:relative) %>
      <% end %>

or:

    <% Comfy::Cms::Site.first.pages.root.children.published.each do |page| %>
      <li><%= link_to page.label, page.url(:relative) %></li>
    <% end %>

***

## Children pages for nested menus
by [Pablo Fernandez](http://www.onboardinglab.com)

`_navigation_links.slim`:
```slim
ul#js-navigation-menu.navigation-menu.show
  == render partial: 'layouts/navigation_link', collection: Comfy::Cms::Site.first.pages.root.children.published, as: :page
```

`_navigation_link.slim`:
```slim
- classes = 'nav-link'
- if page.children.any?
  - classes << ' more'
li[class=classes]
  a[href=page.full_path]= page.label
  - if page.children.any?
    ul.submenu
      == render partial: 'layouts/navigation_link', collection: page.children.published, as: :page
```