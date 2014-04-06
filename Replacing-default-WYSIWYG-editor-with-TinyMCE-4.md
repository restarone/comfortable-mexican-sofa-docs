**!!! TineMCE-4 is work in progress, please be very careful applying this to a production setup. Better go for [TinyMCE-3](https://github.com/comfy/comfortable-mexican-sofa/wiki/Replacing-default-WYSIWYG-editor-with-TinyMCE-3).**

* Add this to your Gemfile:
```
gem 'tinymce-rails', :git => 'git@github.com:spohlenz/tinymce-rails.git', :branch => 'tinymce-4'
```
* Optionally, add [i18n support](https://github.com/spohlenz/tinymce-rails-langs/tree/tinymce-4):
```
gem 'tinymce-rails-langs', :git => 'git@github.com:spohlenz/tinymce-rails-langs.git', :branch => 'tinymce-4'

```
* Include assets accordingly in `app/assets/javascripts/application.js` (we are going to use the jquery version):
```
//= require tinymce
```
* Run bundler:
```
$ bundle install
```
* Create coffeescript file at `app/assets/javascript/comfortable_mexican_sofa/admin/application.js.coffee`:
```coffee
#= require tinymce

window.CMS.wysiwyg = ->
  tinymce.init
    selector: 'textarea[data-cms-rich-text]'
    # any additional tinymce configuration can go here
```

* tinymce-rails-langs will use the current locale. You may set `language` to override:

```
    # any additional tinymce configuration can go here
    language: 'de'
```

* Optionally enable [plugins](http://www.tinymce.com/wiki.php/Plugins) (please see the [TinyMCE documentation](https://github.com/spohlenz/tinymce-rails/blob/tinymce-4/README.md) for further info):

```
    plugins: 'autosave anchor image charmap contextmenu fullscreen link paste preview print visualchars'
```

* Delete `app/assets/javascript/comfortable_mexican_sofa/admin/application.js` if it exists. If you have stuff defined in there you need to migrate it to coffeesript as comfy will use that first (and exclusivley then).
