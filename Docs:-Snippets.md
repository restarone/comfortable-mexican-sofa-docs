## Overview

Snippets are reusable pieces of content that you'd want to manage from Sofa.
Things like copyright notices, maybe even more complex things like navigations.
When you create a snippet you need to provide a unique identifier. For our
example we'll use 'copyright'. Then we can use this snippet in our layout like so:

```html
<html>
  <body>
    {{ cms:markdown content }}
    <div class='footer'>
      {{ cms:snippet copyright }}
    </div>
  </body>
</html>
```

If you ever need to access snippet content from inside your app you can use this
helper: `<%= cms_snippet_content('copyright') %>`. Sometimes you need to provide
the site (if you have more than one): `<%= cms_snippet_content('copyright', @cms_site) %>`
