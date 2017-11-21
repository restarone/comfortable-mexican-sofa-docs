## Overview

When setting up Sofa for the first time you'll be prompted to create a Site.
At the very least you'll need to populate the hostname. If you wish to serve
all content from a particular path (say, http://example.org/en), you would want
to set the path to "en". You can go even deeper, e.g., `en/content/to/read`.
The label is the name of the site; identifier will be automatically
generated from this by default.

### Multiple Sites

As a default Comfortable Mexican Sofa can handle several sites from a single
installation. Each site has its own set of layouts, pages, files, and snippets.
A site is identified by its hostname and path. For example, you can have two
sites with different hostnames, like en.example.org and fr.example.org; or
sites with the same hostname but different paths, like example.org/en and
example.org/fr.

### Localization

When creating a site you can choose one of the provided languages. This will
translate all admin views and set the `I18n.locale` setting in the admin
controller/views.

If you want to force the admin area to use a particular locale that is different from the site language, set the initializer value `config.admin_locale = :en`. Only the admin area will be affected; the site locale settings will still apply.

If you wish to include a locale that doesn't exist yet, take a peek in
[/config/locales](https://github.com/comfy/comfortable-mexican-sofa/tree/master/config/locales). You can create your own and extend Sofa's initialization config;
for example, `config.locales.merge!(arr: 'Pirate')`. Also you're welcome to
contribute your translations to Sofa.
