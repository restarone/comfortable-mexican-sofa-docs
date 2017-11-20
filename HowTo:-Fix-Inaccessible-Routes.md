Because of Comfy's globbing route it's possible that routes pulled in from other
Rails engines are not accessible. It's easy to see when running `rails routes`.
If `comfy_cms_render_page` is not last - you have a problem.

You should be able to resolve it by changing loading priority for the offending
engine. Add this line to `config/application.rb`

```ruby
config.railties_order = [Foo::Engine, :all, :main_app]
```

The idea is that you want all routes defined before you drop Comfy's globbing
route.
