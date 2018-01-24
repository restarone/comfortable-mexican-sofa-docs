## Overview

Layout defines content areas for the page. For example, if you need a page with header, footer, and some content you'd need something like this:

```html
<html>
  <body>
    <div class='header'>
      {{ cms:text header }}
    </div>
    <div class='content'>
      <h1> {{ cms:text header }} </h1>
      {{ cms:markdown content }}
    </div>
    <div class='footer'>
      {{ cms:snippet footer }}
    </div>
  </body>
</html>
```

If this layout is chosen during page creation you will notice that you are
presented with form fields that correspond to the tags defined in the layout
content. In this case you'll have a *header* text field and *content* text area.
When page is rendered, tags are replaced with content that you defined.

### Application Layout

In most cases you'll want to use stylesheets/javascripts and general html layout
that you already have in your application. For that it's enough to select an
*App Layout*. It will be listed as a file that is found in `/views/layouts` when you edit a layout in Sofa.
This way you limit exposure of what can be managed in Sofa. Let's say your
application layout is `application.html.haml`:

```html
!!! html
%html
  %head
    = render 'layouts/head'
  %body
    = render 'layouts/header'
    .content
      = yield
    = render 'layout/footer'
```

Now we don't need to worry about anything but the small bits of HTML.
We can simplify our layout to:

```html
  <h1>{{ cms:text title }}</h1>
  {{ cms:markdown content }}
```

### Nested Layouts

Let's say you need to define a CMS Layout that has left and right columns.
It looks exactly like your one-column layout, but now there's two. You could
just copy-paste it and modify it, but that's not really good. Remember the
often-used `{{ cms:markdown content }}` tag? Content tags with _content_ label
allow layout nesting. *Note:* Tag type could be markdown, wysiwyg, textarea,
text, or whatever as long it's a Fragment based tag with `content` label.

Based on the previous examples this is what two-column layout would look like:

```html
<div class='left'> {{ cms:markdown left_column }} </div>
<div class='right'> {{ cms:markdown right_column }} </div>
```

But what about the _Title_? If you specify our first layout as a parent in
actuality you are dealing with layout that has this content:

```html
<h1> {{ cms:text title }} </h1>
<div class='left'> {{ cms:markdown left_column }} </div>
<div class='right'> {{ cms:markdown right_column }} </div>
```

What happened here is that content of this layout is merged into the parent
via `{{ cms:markdown content }}` tag. You can have multiple levels of nesting
if you so desire.

### CSS and JS

You can manage CSS right here in Sofa. Helps in those cases when you need to
move that logo 2px to the left without redeploying the application. The trick is
to somehow link that resource to the page. You'll notice that you have routes
available:

```
comfy_cms_render_css  GET /cms-css/:site_id/:identifier(/:cache_buster)(.:format)
comfy_cms_render_js   GET /cms-js/:site_id/:identifier(/:cache_buster)(.:format)

```

So all you need to do is link to a proper path. So if your site has _id_ `1` and
layout identifier is `default` the path to css will be: `/cms-css/1/default.css`.
Same applies to javascript link.

If you're not using application layout, you can output CMS managed css and js
like so:

```html
<html>
  <head>
    ...
    {{ cms:asset layout_identifier, type: css, as: tag }}
  </head>
  <body>
    ...
    {{ cms:asset layout_identifier, type: js, as: tag }}
  </body>
</html>
```

If you use application layout, this is how you'd link assets:

```ruby
  = stylesheet_link_tag comfy_cms_render_css_path(@cms_site.id, @cms_layout.identifier)
  = javascript_include_tag comfy_cms_render_js_path(@cms_site.id, @cms_layout.identifier)
```
