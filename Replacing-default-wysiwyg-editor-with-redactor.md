Getting [Redactor WYSIWYG editor](http://imperavi.com/redactor/) working with CMS (version 1.8.1+)

While this editor is not free, it has a number of neat features. Big one is image embedding.

Due to licensing I can't ship CMS with this editor. However now it's easy to integrate in few easy steps.

* Use version 1.12.2 of Comfortable Mexican Sofa due to changes in recent version not supporting the script provided on this page.

* Download Redactor: http://imperavi.com/redactor/download/. No more trial version unfortunately. It's a good editor though, worth the money.

* Within your application create `/app/assets/javascripts/comfortable_mexican_sofa/admin/application.js.coffee` and paste this in:

```coffeescript
#= require comfortable_mexican_sofa/lib/redactor

window.CMS.wysiwyg = ->
  csrf_token = $('meta[name=csrf-token]').attr('content');
  csrf_param = $('meta[name=csrf-param]').attr('content');
  if (csrf_param != undefined && csrf_token != undefined)
    params = csrf_param + "=" + encodeURIComponent(csrf_token)
  
  $('textarea[data-cms-rich-text]').redactor
    minHeight: 400
    buttons: ['formatting', '|', 'bold', 'italic', '|', 'unorderedlist', 'orderedlist', '|', 'image', 'link']
    imageUpload: $('.cms-files-modal').data('iframe-src') + '?ajax=1'
    imageGetJson: $('.cms-files-modal').data('iframe-src') + '?ajax=1'
    formattingTags: ['p', 'h1', 'h2', 'h3', 'h4']
```

* Move `redactor.js` to `/app/assets/javascripts/comfortable_mexican_sofa/lib/`

* Within your application create `/app/assets/stylesheets/comfortable_mexican_sofa/admin/application.css.sass` and paste this:
```sass
//= require comfortable_mexican_sofa/lib/redactor
```

* Move `redactor.css` to `/app/assets/stylesheets/comfortable_mexican_sofa/lib/`

Now all `{{cms:page:label:rich_text}}` fields will be rendered with Redactor.


Some pages use CodeMirror by default i.e. `textarea[data-cm-mode]`.
To override that just override  `window.CMS.codemirror` in your `application.js`. See [application.js.coffee](https://github.com/comfy/comfortable-mexican-sofa/blob/master/app/assets/javascripts/comfortable_mexican_sofa/application.js.coffee)