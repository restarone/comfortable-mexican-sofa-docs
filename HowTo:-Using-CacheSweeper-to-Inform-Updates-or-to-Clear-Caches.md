You can use CacheSweepers to inform about page/site updates or to clear cache.

## Adding Sweepers to Rails 5

In Rails 4, Sweepers have been moved into a separate gem [rails-observers](https://github.com/rails/rails-observers)

Their use is described [here](https://github.com/rails/rails-observers#action-controller-sweeper)

## Configuring sweepers

In your comfortable_mexican_sofa.rb

```
# A class that is included as a sweeper to admin base controller if it's set
# You could also give a array of sweepers
config.admin_cache_sweeper = CmsAdminSweeper
```

## Example of sweeper

Autoload this class somewhere.

```ruby
class CmsAdminSweeper < ActionController::Caching::Sweeper
  # observe Comfy::Cms::Page, Comfy::Cms::Layout, Comfy::Cms::Snippet

  def after_create(model)
    do_sweeping(model)
  end

  def after_update(model)
    do_sweeping(model)
  end

  def after_destroy(model)
    do_sweeping(model)
  end

  def do_sweeping(model)
    # return unless modification is made from controller action
    return false if session.blank? || assigns(:site).blank?

    Rails.logger.info("CmsAdminSweeper.do_sweeping in progress...")

    @model = model
    @site = assigns(:site) # CmsAdminController always assigns site

    # Create OtherEmail emailer to send updates
    OtherEmails.message_to_admin("#{@site.hostname} cms update: #{model.inspect}").deliver

    # Create your own CmsHelper to expire caches you want
    CmsHelper.cms_cache_expire_for_locale()
  end
end

```