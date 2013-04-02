**Note:** This is no longer issue in > 1.8.0 as routes are defined inside your application `routes.rb` file.

ComfortableMexicanSofa uses a catchall route to respond to requests for CMS pages. It places this at the end of its routes, to avoid clobbering any other routes.

Normally this works fine, but if you have many engines included in your application, comfortable mexican sofa's routes may be included in an arbitrary order, and even though the catch-all comes after your main_app, and all the other CMS routes, it will still clobber the routes of any engine that comes after ComfortableMexicanSofa.

In this case, add the following code to application.rb to force CMS to have lowest priority:
```ruby
config.railties_order = [ :all, ComfortableMexicanSofa::Engine ]
```
