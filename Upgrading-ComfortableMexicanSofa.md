To upgrade to a newer version of ComfortableMexicanSofa you must bump up the version number in your Gemfile like so:

    gem 'comfortable_mexican_sofa', '>=1.3.0'

and run `bundle install`. 

It's also a good idea to run `rails generate cms` to update the initializer or image/css/js assets (if using Rails3.0). Sometimes you'll need to create migrations to adjust the database. Generally it happens during major and minor version changes. Meaning that upgrade from 1.1.5 to 1.2.2 will probably require a migration, but 1.1.5 to 1.1.9 will not. If upgrading several minor version you'll need to apply all database migrations sequentially.

## Upgrading from 1.0.x to 1.1.1
* There was slight reorganization of internals so there's a quick migration to make everything work again: [[https://github.com/twg/comfortable-mexican-sofa/raw/fixtures/db/migrate/upgrades/02_upgrade_to_1_1_0.rb]]. Just create a new migration, paste content of the above file and `rake db:migrate`.
* Some initializer settings got changed/removed. See: [[https://github.com/twg/comfortable-mexican-sofa/raw/master/config/initializers/comfortable_mexican_sofa.rb]]
* `CmsSite`, `CmsLayout`, `CmsPage`, `CmsSnippet` are changed to `Cms::Site`, `Cms::Layout`, `Cms::Page` and `Cms::Snippet`. It only matters if you directly manipulate those objects somehow.

## Upgrading from 1.1.x to 1.2.0
* Revision system is introduced and that's why you need to grab this migration: [[https://github.com/twg/comfortable-mexican-sofa/raw/master/db/migrate/upgrades/03_upgrade_to_1_2_0.rb]]. Just create a new migration, paste content of the above file and `rake db:migrate`.
* New initializer setting is added `revisions_limit`: [[https://github.com/twg/comfortable-mexican-sofa/raw/master/config/initializers/comfortable_mexican_sofa.rb]]

## Upgrading from 1.2.x to 1.3.0
* Multiple Sites is a default functionality now. Setting to toggle it in the initializer is gone. `content_prefix_path` is an attribute of the Site now. This way if you want to serve pages from `http://localhost/en/` you need to set up a Site with **hostname** `localhost` and **path** `en`.
* Migration file can be found here: [[https://github.com/twg/comfortable-mexican-sofa/raw/master/db/migrate/upgrades/04_upgrade_to_1_3_0.rb]]
* Page caching (along with the initializer setting) is removed for the time being as it doesn't work for multiple sites.