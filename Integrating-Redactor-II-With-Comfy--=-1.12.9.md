## Asset Overrides

In order to replace the bundled version of redactor (Redactor 1) you must override several files with versions downloaded with your purchase of Redactor II.

| Download Source | Where to place in app |
| --------------- | --------------------- |
| https://imperavi.com/redactor/buy/ | `app/assets/javascripts/comfy/admin/cms/lib/redactor.js`|
| https://imperavi.com/redactor/buy/ | `app/assets/stylesheets/comfy/admin/cms/lib/redactor.css` |
| https://imperavi.com/redactor/plugins/definedlinks/ | `app/assets/javascripts/comfy/admin/cms/lib/redactor/definedlinks.js` |
| https://imperavi.com/redactor/plugins/filemanager/ | `app/assets/javascripts/comfy/admin/cms/lib/redactor/filemanager.js` |
| https://imperavi.com/redactor/plugins/imagemanager/ | `app/assets/javascripts/comfy/admin/cms/lib/redactor/imagemanager.js` |
| https://imperavi.com/redactor/plugins/table/ | `app/assets/javascripts/comfy/admin/cms/lib/redactor/table.js` |
| https://imperavi.com/redactor/plugins/video/ | `app/assets/javascripts/comfy/admin/cms/lib/redactor/video.js` |

## Controller Overrides

Redactor II also expects a slightly different JSON syntax for the filemanager/imagemanager plugins, so it is necessary to override the format returned in `Comfy::Admin::Cms::FilesController`.

A full example of this controller (as of `1.12.9`) can be found here: https://gist.github.com/mattmueller/0b933bf64b7bc1d419cc369ea48a1d11

The important changes take place between lines 14 and 28...namely:
 * adding the `id` attribute
 * switching the `image` key to `url` for image requests
 * switching the `link` key to `url` for file requests

This controller can be replaced by placing it at `app/controllers/comfy/admin/cms/files_controller.rb`.

## Further customization

You can further customize the toolbar, options, etc. by overriding `window.CMS.wysiwyg` in `custom.js` or elsewhere.

The default definition (as of `1.12.9`) can be found here: https://github.com/comfy/comfortable-mexican-sofa/blob/master/app/assets/javascripts/comfy/admin/cms/base.js.coffee#L75