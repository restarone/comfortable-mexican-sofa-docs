## Quick Start Guide

Assuming that you followed steps to install everything, start the server:

```bash
rails s
```

Now visit http://localhost:3000/admin
You'll be prompted to enter username and password. Default authentication
credentials are: **username** and **password**.

You should change default credentials by editing [/config/initializers/comfortable\_mexican\_sofa.rb](https://github.com/comfy/comfortable-mexican-sofa/blob/master/config/initializers/comfortable_mexican_sofa.rb):

```ruby
ComfortableMexicanSofa::AccessControl::AdminAuthentication.username = 'username'
ComfortableMexicanSofa::AccessControl::AdminAuthentication.password = 'password'
```

You'll be prompted to create a *Site*. If you're not planning to have multi-homed
setup, nothing here matters other than *label* and *identifier*. Create *Site* and
you'll be redirected to *Layout* creation view.

Give *Layout* a *label* and *identifier*. You'll notice that *content* is already
pre-filled with

```ruby
{{ cms:wysiwyg content}}
```

This just means that *Pages* using this layout will have a single text field
that is presented in a Wysiwyg editor in the admin area.

*Layouts* may have many more content tags decorated with HTML content. A simple
example may look something like this:

```html
<h1>{{ cms:text header }}</h1>
{{ cms:file header-image, as: image, resize: "400x50^" }}
<div class="row">
  <div class="col-md-6">
    {{ cms:markdown left-column }}
  </div>
  <div class="col-md-6">
    {{ cms:markdown right-column }}
  </div>
</div>
```

Once you have *Layout* ready you may start creating pages. Pages editing view
should reflect the *Layout* chosen.
