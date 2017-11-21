## Content Management Overview

In most basic form, *Page* has content that we can edit in admin area and then
it gets rendered when page is requested from the public side.

Page may contain one or more Fragments. Fragments hold content that can be either
text or file attachments. Placement of those fragments is defined on the *Layout*
via content tags that look something like this `{{ cms:tag_name param, foo: bar }}`.

Minimal *Layout* may hold this kind of content:

```
{{ cms:textarea content }}
```

This means that all pages using this *Layout* will have a single fragment that
is managed via textarea in the admin area.

Layouts may have more complicated structure. For example:

```html
<h1>{{ cms:text header }}</h1>
{{ cms:file header-image, as: image, resize: "400x50^" }}
<div class="row">
  <div class="col-md-6">
    {{ cms:markdown left-column }}
  </div>
  <div class="col-md-6">
    {{ cms:wysiwyg right-column }}
  </div>
</div>
```

Pages using this Layout will have:

* text input for header title
* file upload field for header-image
* markdown editor textarea for left-column
* wysiwyg editor textarea for right-column

When page is requested, it will be rendered into something like this:

```html
<h1>Page Title</h1>
<img src="/rails/active_storage/foo/bar" />
<div class="row">
  <div class="col-md-6">
    Left Content
  </div>
  <div class="col-md-6">
    Right Content
  </div>
</div>
```

Not all content tags are tied to Page Fragments. Some are wrappers for view
helpers, partials, etc. Anything that can output some text to be inserted into
page structure.

Those tags can be inserted anywhere: Layouts, Pages, Snippets. For example, you
can define tags inside Page content, like: `{{cms:snippet email-button }}`.
This will render content of that snippet wherever this tag is defined.

Read entry on Content Tags for more info and examples.
