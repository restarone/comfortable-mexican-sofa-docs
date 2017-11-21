## Instance Variables

When rendering partials and helpers from CMS, you have access to `@cms_site`,
`@cms_layout` and `@cms_page`. For example, you can probably use the page object
to render a navigation bar. The application layout also has access to those
variables if used in `Comfy::Cms::Layout`.

## Helper Methods

*Note:* If your app has `config.action_controller.include_all_helpers = false`
make sure you have `helper Comfy::CmsHelper` defined in your `ApplicationController`.

There are four helper methods available: `cms_fragment_content()`,
`cms_fragment_render()` and more frequently used `cms_snippet_content()` and `cms_snippet_render()`.

Difference between `content` and `render` is that `render` does tag expansion.
So if you have tags defined inside your fragment/snippet you want to use `render`
variant. Be aware that it might be slow if you have a lof of things going on there.

`cms_fragment_content` is used to access content inside page fragments. If you
have a page that has its content stored against
`{{cms:markdown content, render: false}}` you can easily retrieve it like so:
`cms_fragment_content(:content)`. If you want to use this method outside CMS
rendering, like in your own view/controller, you need to provide a
`Comfy::Cms::Page` object:
`cms_fragment_content(:content, Comfy::Cms::Page.find_by_full_path('/herp/derp'))`

For instance, if you want to get the URL for an image attached as a fragment
attachment, you can use:

```erb
<% img_url = cms_fragment_render(:icon, @cms_page) %>
```

Similarly, you can get the snippet content with `cms_snippet_content(:example)`
if you have a Comfy::Cms::Snippet with slug 'example'. Once again, outside of CMS
rendering you may need to provide `Comfy::Cms::Site` object (although it's
usually found automatically):
`cms_snippet_content(:example, Comfy::Cms::Site.find_by_hostname('example.com'))`
