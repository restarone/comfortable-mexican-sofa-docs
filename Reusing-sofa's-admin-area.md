If you wish, you can re-use Sofa's admin area for things you need to administer in your application. To do this, first you will need to make your admin controllers to inherit from CmsAdmin::BaseController. This way, your admin views will be using Sofa's admin layout and it's basic HttpAuth.
    
    class Admin::CategoriesController < CmsAdmin::BaseController
      # your code goes here
    end
    
From your views you can use `cms_form_for` method to re-use Sofa's FormBuilder. There are also some existing styles for tables, will\_paginate helpers, etc. Take a look in [/public/stylesheets/comfortable\_mexican\_sofa/content.css](https://github.com/twg/comfortable-mexican-sofa/blob/master/public/stylesheets/comfortable_mexican_sofa/content.css)

You will probably want to add a navigation link on the left side, and for that you will want to use ViewHook functionality. Create a partial that has a link to your admin area and declare in Sofa's initializer: `ComfortableMexicanSofa::ViewHooks.add(:navigation, '/admin/navigation')`. Similarly you can add extra stylesheets, etc into admin area in the same way.