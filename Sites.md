### Set up
When setting up Sofa for the first time you'll be prompted to create a Site. At the very least you'll need to populate the *hostname*. If you wish to serve all content from a particular path, like `http://example.org/en/` you want to set *path* to `en`. You can go even deeper, like so: `en/content/to/read`

### Multiple Sites
As a default ComfortableMexicanSofa can handle several sites from a single installation. Each site has it's own set of layouts, pages and snippets. Site is identified by it's hostname and path. For example you can have two sites with different hostnames like: `en.example.org` and `fr.example.org`; or sites with same hostname but different paths: `example.org/en` and `example.org/fr`

### Localization
When creating a site you can choose one of the provided languages. This will translate all admin views and set `I18n.locale` setting in the controller/views. Handy when you need to render your own partials/helpers from the CMS managed content.

If you want to force admin area to a particular locale (like English), disregarding the site language, see the initializer and set `config.admin_locale = :en`. This will only keep admin area to specified locale, during page rendering Site locale will still apply.

### Mirroring
When you have two or more sites that need to share same structure (think different languages) you should enable mirroring on those sites. This will automatically sync layouts, pages and snippets with same slugs and paths for all sites that are marked as *mirrors*. For example, if you create page `/welcome` on Site A, Site B will also have this page created. Content of the page on Site B will be blank however, you'll need to populate it.



