## Content Tags Overview

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


## Other Tags
### Snippet


### Helper


### Partial


### FileLink


### Asset





