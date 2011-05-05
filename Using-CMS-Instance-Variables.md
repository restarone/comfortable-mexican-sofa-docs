# Using CMS Instance Variables

When rendering CMS content you have access to the following instance variables: `@cms_site`, `@cms_layout` and `@cms_page` from helpers, partials and application layouts used during rendering.

### @cms_site

This is the instance variable for CMS Site object. Generally you don't really need to worry about this one unless you have multiple [[Sites]]. You can use it for things like generation of the primary navigation:

    <% @cms_site.pages.root.children.published.each do |page| %>
      <%= link_to page.label, page.full_path %>
    <% end %>
    
### @cms_layout
Not particularly useful, but you can grab CSS/JS associated with the CMS Layout, or all pages that use this Layout.

### @cms_page
CMS Page instance variable. All the information you need about the page that is currently being rendered. Some useful methods: `label`, `full_path`, `content`

    