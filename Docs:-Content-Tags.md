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

### Text, TextArea, Markdown and Wysiwyg

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
attachments to non-persisted record. However, take care with removing those
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


### Date and Datetime


### Checkbox


### Files and File


## Other Tags
### Snippet


### Helper


### Partial


### FileLink


### Asset


### NonRenderable Fragments


## Content Tag Namespaces

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
