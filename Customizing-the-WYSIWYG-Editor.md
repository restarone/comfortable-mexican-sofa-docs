Sofa allows you to override the default buttons that appear on the JS rich_text/WYSIWYG editor.

Use [ViewHooks](../../comfortable-mexican-sofa/wiki/Reusing-sofa%27s-admin-area) to link up a JS file in Sofa's Head with the following:

`$.CMS.config['elRTE']['toolbar'] = [];` 

Fill the blank array with the items you'd like in the toolbar. 

For example, to use HTML table controls, you'd specify:

`$.CMS.config['elRTE']['toolbar'] = ['tables'];`

### Getting the WYSIWYG (Redactor) to not add paragraph on new lines
In your custom.js.coffee, you need to add the following line: 

```
if window.CMS != undefined && window.CMS.wysiwyg != undefined
  window.CMS.wysiwyg = ->
    csrf_token = $('meta[name=csrf-token]').attr('content')
    csrf_param = $('meta[name=csrf-param]').attr('content')

    if (csrf_param != undefined && csrf_token != undefined)
      params = csrf_param + "=" + encodeURIComponent(csrf_token)

    $('textarea.rich-text-editor, textarea[data-cms-rich-text]').redactor
      minHeight:          160
      autoresize:         true
      imageUpload:        "#{CMS.file_upload_path}?source=redactor&type=image&#{params}"
      imageManagerJson:   "#{CMS.file_upload_path}?source=redactor&type=image"
      fileUpload:         "#{CMS.file_upload_path}?source=redactor&type=file&#{params}"
      fileManagerJson:    "#{CMS.file_upload_path}?source=redactor&type=file"
      definedLinks:       "#{CMS.pages_path}?source=redactor"
      buttonSource:       true
      paragraphize:       false
      replaceDivs:        false
      removeWithoutAttr:  false
      lang:               CMS.locale
      formatting:         ['p', 'h1', 'h2', 'h3', 'h4', 'h5', 'h6']
      plugins:            ['imagemanager', 'filemanager', 'table', 'video', 'definedlinks']
```

Look up https://github.com/comfy/comfortable-mexican-sofa/blob/master/app/assets/javascripts/comfy/admin/cms/lib/redactor.js for various options that you would like to change. 

## Replacing wysihtml5 with a different WYSIWYG editor
* [[Replacing-default-wysiwyg-editor-with-redactor]]