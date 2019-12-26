## Dependencies

* Rails 5.2 or 6.0
* File attachments are handled by [ActiveStorage](https://github.com/rails/rails/tree/master/activestorage). You will need to copy over database migrations by running
  `rails active_storage:install`
* To resize attached images you'll need to have [ImageMagic](http://www.imagemagick.org/script/download.php) installed.
* Pagination is handled by either [Kaminari](https://github.com/kaminari/kaminari) or [WillPaginate](https://github.com/mislav/will_paginate). Make sure you have one
  defined in your Gemfile.

## Installation

Add to the Gemfile of your Rails project:

```ruby
gem 'comfortable_mexican_sofa', '~> 2.0.0'
```

Then from your Rails project's folder run these commands:

```bash
bundle install
rails generate comfy:cms
rake db:migrate
```

The generator will create the initializer, database migration, example CMS Seeds and will move route sets.

Take a look at `routes.rb` and make sure that the content serving route appears last:

```ruby
comfy_route :cms_admin, path: '/admin'
comfy_route :cms, path: "/"
```

*Note:* All routes appearing after `comfy_route :cms` will not be accessible as it's a
[globbing route](http://guides.rubyonrails.org/routing.html#route-globbing-and-wildcard-segments). This includes routes included
by other Rails Engines. Make sure that everything looks ok by running `rails routes`
and confirming that `comfy_cms_render_page` appears last.
