## Basics

If you wish, you can re-use Sofa's admin area for things you need to administer in your application. To do this, first you will need to make your admin controllers to inherit from Admin::Cms::BaseController. This way, your admin views will be using Sofa's admin layout and it's basic HttpAuth.
    
    class Admin::CategoriesController < Admin::Cms::BaseController
      # your code goes here
    end
    
## Scaffold Generator

Easiest way to generate your admin crud interface is to run `rails g comfy:scaffold`. Works pretty much the same way as a standard Rails scaffold generator. For example let's generate admin area for Locations. Simply run something like this: `rails g comfy:scaffold Location name:string distance:integer`. After running it you should get:

* `db/migrate/create_locations.rb` migration file. Don't forget your indexes.
* `app/models/location.rb` model file
* `test/fixtures/locations.yml` test fixture file
* `test/models/location_test.rb` actual tests for Location. Has a `assert_errors_on` helper call. Replace with what works for you.
* `app/controllers/admin/locations_controller.rb` admin controller
* `test/controllers/admin/locations_controller_test.rb` tests for the admin controller. Remember you need to authenticate use there. If you are using default BasicAuth have something like this in your setup: `@request.env['HTTP_AUTHORIZATION'] = "Basic #{Base64.encode64('username:password')}"`
* `app/views/admin/locations/` with all the views
* `routes.rb` will be updated, but you want to put new route in a proper spot.
* `app/views/admin/cms/partials/_navigation_inner.html.haml` will be updated/created to add link to the side nav