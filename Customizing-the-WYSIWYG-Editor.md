Sofa allows you to override the default buttons that appear on the JS rich_text/WYSIWYG editor. For more information on the available buttons and panels, visit http://elrte.org/redmine/projects/elrte/wiki/Docs_EN#Custom-toolbar

Use [ViewHooks](../../comfortable-mexican-sofa/wiki/Reusing-sofa%27s-admin-area) to link up a JS file in Sofa's Head with the following:

`$.CMS.config['elRTE']['toolbar'] = [];` 

Fill the blank array with the items you'd like in the toolbar. 

For example, to use HTML table controls, you'd specify:

`$.CMS.config['elRTE']['toolbar'] = ['tables'];`

### Getting the WYSIWYG (Redactor) to not add paragraph on new lines
In your custom.js.coffee, you need to add the following line: 

`if window.CMS != undefined && window.CMS.wysiwyg != undefined
  window.CMS.wysiwyg = ->
    $('textarea.rich-text-editor, textarea[data-cms-rich-text]').redactor
      paragraphize: false`

## Replacing wysihtml5 with a different WYSIWYG editor
* [[Replacing-default-wysiwyg-editor-with-redactor]]