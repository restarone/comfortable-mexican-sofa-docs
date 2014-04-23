## Installation
Add to the Gemfile of your Rails project:
```bash
gem 'comfortable_mexican_sofa'
```
    
Then from your Rails project's folder run these commands:
```bash
bundle install
rails generate comfy:cms
rake db:migrate
```

The generator will create the initializer, database migration, example CMS fixtures and will move route sets.

Take a look at `routes.rb` and make sure that the content serving route appears last:

```ruby
comfy_route :cms_admin, :path => '/admin'
comfy_route :cms, :path => '/', :sitemap => false
```

If you are upgrading from an older version of ComfortableMexicanSofa, please take a look at [[Upgrading ComfortableMexicanSofa]].

## Quick Start Guide

Run the default web server:
```ruby
rails server
```
Now visit **http://0.0.0.0:3000/admin** and you should be able to connect with **username** and **password**.

You can change the default credentials by editing [/config/initializers/comfortable\_mexican\_sofa.rb](https://github.com/comfy/comfortable-mexican-sofa/blob/master/config/initializers/comfortable_mexican_sofa.rb):

```ruby
ComfortableMexicanSofa::HttpAuth.username = 'username'
ComfortableMexicanSofa::HttpAuth.password = 'password'
```

Before we can populate the site with content, we will need to create a Site. The Site is what defines the hostname, content path, and the language. After creating a Site, you need to make a Layout, which is the template for your content; allowing you to define reusable content (such as the header and footer) and placeholders for content.

A very simple Layout can look like this:
```html
<html>
  <body>
    <h1>{{ cms:page:header:string }}</h1>
    {{ cms:page:content:text }}

    <!-- You can add as many blocks as you want -->
    {{ cms:page:another_block:rich_text }}
  </body>
</html>
```

Once you have a layout, you may start creating pages and populating content. It's that easy.