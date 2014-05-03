* Add this to your Gemfile:
```
gem 'tinymce-rails', '~> 3.0'
```
* Optionally, add [i18n support](https://github.com/spohlenz/tinymce-rails-langs/):
```
gem 'tinymce-rails-langs'
```
* Include assets accordingly in `app/assets/javascripts/application.js`:
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

* Optionally enable [plugins](http://www.tinymce.com/wiki.php/TinyMCE3x:Plugins) (please see the [TinyMCE documentation](https://github.com/spohlenz/tinymce-rails/blob/master/README.md) for further info):

```
    plugins: 'autosave anchor image charmap link paste preview print visualchars'
```

* Delete `app/assets/javascript/comfortable_mexican_sofa/admin/application.js` if it exists. If you have stuff defined in there you need to migrate it to coffeesript as comfy will use that first (and exclusivley then).
