Getting [Redactor WYSIWYG editor](http://imperavi.com/redactor/) working with CMS.

Due to licensing I can't ship CMS with this editor. However now it's easy to integrate in few easy steps.

* Download Redactor: http://imperavi.com/redactor/download/. Sign up to get the trial version to begin with.

* Within your application create `/app/assets/javascripts/comfortable_mexican_sofa/admin/application.js.coffee` and paste this in:

```coffeescript
#= require comfortable_mexican_sofa/lib/redactor

window.CMS.wysiwyg = ->
  csrf_token = $('meta[name=csrf-token]').attr('content');
  csrf_param = $('meta[name=csrf-param]').attr('content');
  if (csrf_param != undefined && csrf_token != undefined)
    params = csrf_param + "=" + encodeURIComponent(csrf_token)
  
  $('textarea[data-rich-text]').redactor
    minHeight: 400
    buttons: ['formatting', '|', 'bold', 'italic', '|', 'unorderedlist', 'orderedlist', '|', 'image', 'link']
    imageUpload: "#{CMS.file_upload_path}?ajax=1&#{params}"
    imageGetJson: "#{CMS.file_upload_path}?ajax=1"
    formattingTags: ['p', 'h1', 'h2', 'h3', 'h4']
```

* Move `redactor.js` to `/app/assets/javascripts/comfortable_mexican_sofa/lib/`

* Within your application create `/app/assets/stylesheets/comfortable_mexican_sofa/admin/application.css.sass`
```sass
//= require comfortable_mexican_sofa/lib/redactor
```

* Move `redactor.css` to `/app/assets/stylesheets/comfortable_mexican_sofa/lib/`

