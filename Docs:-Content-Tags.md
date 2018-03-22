## Content Tags Overview

* [{{ cms:text }}](#text-textarea-wysiwyg-and-markdown)
* [{{ cms:textarea }}](#text-textarea-wysiwyg-and-markdown)
* [{{ cms:wisywyg }}](#text-textarea-wysiwyg-and-markdown)
* [{{ cms:markdown }}](#text-textarea-wysiwyg-and-markdown)
* [{{ cms:number }}](#number)
* [{{ cms:date }}](#date-and-datetime)
* [{{ cms:datetime }}](#date-and-datetime)
* [{{ cms:checkbox }}](#checkbox)
* [{{ cms:file }}](#file-and-files)
* [{{ cms:files }}](#file-and-files)
* [{{ cms:snippet }}](#snippet)
* [{{ cms:helper }}](#helper)
* [{{ cms:partial }}](#partial)
* [{{ cms:file_link }}](#filelink)
* [{{ cms:page_file_link }}](#pagefilelink)
* [{{ cms:asset }}](#asset)

Content tags have this structure: `{{ cms:tag_name params }}`. Always wrapped
with double curly brakets: `{{ }}`. Always starts with `cms:`. Immediately
followed by tag name. Params are JSON-like. Comma separated with support for
key/value params.

Values of params can be wrapped with quotes. Here's an example of a valid tag:

`{{ cms:some_tag arg1, "some other argument", key_a: "a,b,c", key_b: value }}`

There are two different type of content tags. Ones that are responsible for page
fragment content management, and others are used to render content that comes
from elsewhere.

## Page Fragment Tags

Following content tags interact with data stored on the `Comfy::Cms::Fragment`
records.

Content of these tags may contain other *non-fragment* tags (don't cross the beams).

### Text, TextArea, Wysiwyg, and Markdown

These tags function the same. Content is stored against `content` attribute of
the page fragment. The only difference is how they get rendered in the admin area.

```
{{ cms:text example }}
```
Text tag content is displayed as a simple text input

```
{{ cms:textarea example }}
```
Textarea tag content is displayed as HTML text editor powered by CodeMirror.

```
{{ cms:wysiwyg example }}
```
Wysiwyg tag content is displayed in Redactor Wysiwyg text editor. Redactor is
capable of handling file and image attachments. Everything uploaded through
this editor will create a *File* tagged as "wysiwyg". This allows creating
attachments to a non-persisted record. However, take care with removing those
files as you can't really tell if any pages actually use them.

Redactor 10.2.5 is a premium editor that has OEM license that allows it to be
used on apps that utilize ComfortableMexicanSofa. While it's not the most current
Redactor, it's the only one I have licence to bundle. But it's great and works
great.

```
{{ cms:markdown example }}
```
Markdown tag content is displayed as Markdown editor powered by CodeMirror.
Fragment content is stored as markdown and converted to HTML when rendered.

### Number
```
{{ cms:number example }}
```
For all those times where you need number input. It still stores it as text though.

### Date and Datetime

```
{{ cms:date example }}
```
Stores content in `datetime` attribute of the page fragment. So it comes out as
a proper DateTime value. Rendered using Flatpickr in the admin area.

```
{{ cms:datetime example }}
```
Same as Date, but with option to set Time!

You can change how datetime is rendered by passing `strftime` option like so:

```
{{ cms:datetime example, strftime: "at %I:%M%p" }}
```

### Checkbox

```
{{ cms:checkbox example }}
```
Allows to set a `boolean` attribute on the page fragment. Displayed as a checkbox
in the admin area. Unchecked by default.

### File and Files

```
{{ cms:file example }}
```
This tag handles attachments on page fragments. Attachments are handled by
[ActiveStorage](https://github.com/rails/rails/tree/master/activestorage). In
the admin area you can select attachments that need to be removed during page
save. File tag will replace existing attachment, if there's one.

This tag accepts several options. Let's go through them:

```
{{ cms:file example, as: image, label: "My Photo", resize: "100x50>", gravity: "center", crop: "100x50+0+0"}}
```
- `as` can be set to following values:
  - `url` - This is the default. Will render URL pointing to uploaded attachment.
  - `link` - Will wrap URL in `<a href=>` tag.
  - `image` - Will wrap URL in `<img src=>` tag.
- `label` - Will use this as text for links or alt attibute value for images.
- `resize`, `gravity`, `crop` - Only applicable for image variants. These are
  transform options that are passed into ImageMagick via ActiveStorage.

```
{{ cms:files example }}
```
Same as "files" tag, all attached files are appended to the existing ones. Out
of the box, you'll probably will be unhappy with its rendered output. I suggest
doing `render: false` and manually rendering files out using view helper.


#### Non-Renderable Fragments

What if you don't want to render content and want to handle it in some other way.
For example meta tags. You don't want to render meta description. Just pass
`render: false` parameter. For example:

```
{{ cms:text meta-description, render: false }}
```

This tag's content will not be rendered out. Now you may manually grab that
fragment's content like this (part of application.html.erb):

```erb
<meta name="description" content="<%= cms_fragment_content("meta-description") %>">
```

#### Content Tag Namespaces

You can organize your page fragments into tabbed sections by passing `namespace`
parameter. If you wanted to organize a set of Open Graph fields into an "Og"
tab, your layout might look something like this:

```html
{{ cms:text title }}
{{ cms:text description }}
...
{{ cms:text open_graph_description, namespace: OG }}
{{ cms:text open_graph_title, namespace: OG }}
```

Comfy will create two tabs in the page editor: Default and OG. The `title` and
`description` fields will be displayed in the Default tab and the two namespaced
fields will be displayed in the OG tab.

#### Localizing Tag Labels and Namespaces

Let's say you have tag like this: `{{ cms:markdown foo, namespace: bar }}`and
would like to localize it for admin area. All you need is to add this entry to
your `config/locales/your_locale.yml` file:

```yml
your_locale:
  comfy:
    cms:
      content:
        tag:
          foo: Localized Foo
        namespace:
          bar: Localized Bar
```

## Other Tags
### Snippet

```
{{ cms:snippet identifier }}
```
Snippet tags are bits of reusable content that can be used anywhere. Imagine
creating content like a sharing widget, or business address that you want to
randomly use across your site.

They are managed in *Snippets* section of the admin area.

### Helper

```
{{ cms:helper some_helper, param_a, key: param_b }}
```
Helper is a wrapper for your regular view helpers. Normally you cannot have ERB
in CMS content, so there are tags that allow calling helpers and partials. All
keys and arguments are strings. Keep that in mind when handling them inside the
helper.

When rendered, this tag will be converted to:

```erb
<%= some_helper("param_a", {"key" => "param_b"}) %>
```

It's possible to set a whitelist of helpers that can be called. There's a default
blacklist of methods that cannot be called this way: `eval`, `class_eval`,
`instance_eval`, and `render`.

### Partial

```
{{ cms:partial "path/to/partial", local_var: "value" }}
```
Same idea as with view helpers. This tag will be converted to:

```erb
<%= render partial: "path/to/partial", locals: {"local_var" => "value"} %>
```
It's possible to define whitelist of partials that can be called via this tag.

### FileLink

```
{{ cms:file_link file_id }}
```

This tag is identical to `file` tag in a way it's rendered. But instead of
dealing with page fragment attachments, it renders previously uploaded files
(`Comfy::Cms::File` records) in *Files* section of the admin area.

### PageFileLink

Similar tag to the `file_link` tag. It allows linking to files uploaded to the
page itself. For example, if your layout has these tags defined:

```
{{ cms:file graphic, render: false }}
{{ cms:files attachments, render: false }}
```
You can link to the files from an individual page (or snippet rendered in
the context of the page) like so:

```
{{ cms:page_file_link graphic }}
{{ cms:page_file_link attachments, filename: "cat.jpg" }}
```

### Asset

```
{{cms:asset layout_identifier, type: css, as: tag}}
```

Mentioned in Layouts section of the Wiki. This is how we can output content
of the Layout's CSS/JS fields into a page.

`type` is either `css` or `js`. `as` can be ommited and only URL will be
rendered out.
