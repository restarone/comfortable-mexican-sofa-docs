# Page Tag

Page tag is defines a piece of content that is displayed during page rendering. Each piece of content has a unique identifier, or `label` and an optional format. Format defines what kind of form field needs to be used during CMS Page creation.

### Available formats

* *{{ cms:page:content }}* - **Text**: Format parameter can be omitted. It defaults to *text*.
* *{{ cms:page:content:text }}* - **Text**: A plain-text textarea. With html/css/js code highlighting provided via CodeMirror
* *{{ cms:page:content:rich\_text}}* - **RichText**: WYSIWYG editor (TinyMCE) will be used.
* *{{ cms:page:content:string }}* - **String**: Sometimes you need a short text entry. This will render a text field.
* *{{ cms:page:content:datetime }}* - **DateTime**: Textfield, with Datetime selection widget.
* *{{ cms:page:content:integer }}* - **Integer**: Input with 'number' type will be rendered. You can only type numbers in there.

Formats only control how content gets populated during CMS Page creation. They do not control how that content is displayed on final page render.
