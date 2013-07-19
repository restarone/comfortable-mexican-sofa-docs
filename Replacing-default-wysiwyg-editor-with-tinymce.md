1. Add this to your Gemfile:
```
gem 'tinymce-rails'
```

2. Run `$ bundle install`

3. Create a file at `app/assets/javascript/comfortable_mexican_sofa/admin/application.js.coffee`:
```coffee
#= require tinymce

window.CMS.wysiwyg = ->
  tinymce.init
    selector: 'textarea[data-rich-text]'
    # any additional tinymce configuration can go here
```