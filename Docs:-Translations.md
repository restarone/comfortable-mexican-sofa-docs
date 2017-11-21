## Overview

All pages may have a translation recods associated with them. Translations are
very similar to Pages as far as content goes. You may choose different Layout
than the Page you're translating though. Translations have Language or `locale`
that are different than the `locale` of the Site.

## How to serve translated pages

CMS content serving controller will automatically select Translation based on
the set `I18n.locale`. Here's a simple setup:

Update `routes.rb` entry to something like this:

```ruby
comfy_route :cms, path: "/:locale/"
```

Then in `application_controller.rb`:

```ruby
before_action :set_locale

def set_locale
  if params[:locale].present?
    I18n.locale = params[:locale]
  else
    I18n.locale = I18n.default_locale
  end
end
```

Now making a request to `/fr/some/page` should serve French translation of that
page (if there's one).

### Note about @cms_page

While Translation is a separate record from Page, we don't handle it on the views.
@cms_page object is mutated with translation data. So you don't need to handle
it in a special way. All view helpers like `cms_fragment_content` should work
without worrying about translations either.
