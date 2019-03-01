### Basics

Before we start, make sure you're familiar with how Rails Engines can be modified.
Please take 2 minutes to read this: http://guides.rubyonrails.org/engines.html#improving-engine-functionality

If you wish, you can re-use Sofa's admin area for things you need to administer
in your application. To do this, first you will need to make your admin
controllers to inherit from Admin::Cms::BaseController. This way, your admin
views will be using Sofa's admin layout and it's basic HttpAuth.


```ruby
class Admin::CategoriesController < Comfy::Admin::Cms::BaseController
  # your code goes here
end
```

### Adding custom JS/CSS to the admin area

After installing CMS you should be able to find `/app/assets/javascripts/comfy/admin/cms/custom.js` and `/app/assets/stylesheets/comfy/admin/cms/custom.sass` in your app. Anything you put in there will be available in all admin views. 

### Scaffold Generator

Easiest way to generate your admin CRUD interface is to run
`rails g comfy:scaffold`. Works pretty much the same way as a standard Rails
scaffold generator. For example let's generate admin area for Locations. Simply
run something like this:

```
rails g comfy:scaffold Location name:string distance:integer
```

-> ISSUE: I found that when using this command one will get most things right out of the box, but in my case i had the problem, that the generated controller missed a ```::Cms::``` derivation so you might have to check if your ```app/models/location.rb``` also has this ```Comfy::Admin::BaseController``` missing the Cms in between Admin and BaseController, so it should look like this ```Comfy::Admin::Cms::BaseController```.
-> Visually you can check if you have this problem if your cms side navigation has options disappearing if you navigate to the newly generated menue point. This dissappearing of menue options should of course not happen and is a cause of the missing derivation.
-> Also one needs to specify at least one model parameter. (With no parameters the template will fail, parameters are in this example the name and the distance.)



After running it you should get:

* `db/migrate/create_locations.rb` migration file. Don't forget your indexes.
* `app/models/location.rb` model file
* `test/fixtures/locations.yml` test fixture file
* `test/models/location_test.rb` actual tests for Location. Has a `assert_errors_on` helper call. Replace with what works for you.
* `app/controllers/admin/locations_controller.rb` admin controller
* `test/controllers/admin/locations_controller_test.rb` tests for the admin controller.
* `app/views/admin/locations/` with all the views
* `routes.rb` will be updated, but you want to put new route in a proper spot.
* `app/views/comfy/admin/cms/partials/_navigation_inner.html.haml` will be updated/created to add link to the side nav

### Changing Views
You can outright modify any view from your application by creating same file with a matching path. However there are a pile of partials that can be used to inject bits of html all over the place. To see what's available change `config.reveal_cms_partials` to `true` and restart application.

### Changing Models/Controllers
If you need to do some serious hacking I recommend forking entire project. You can always do monkey-patching or file overwrites from your application.
