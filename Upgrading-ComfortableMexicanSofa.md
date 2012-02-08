To upgrade to a newer version of ComfortableMexicanSofa you must bump up the version number in your Gemfile like so:

    gem 'comfortable_mexican_sofa', '~>1.6.0'

and run `bundle install`. 

It's also a good idea to run `rails generate comfy:cms` to update the initializer or image/css/js assets (if using Rails3.0). Sometimes you'll need to create migrations to adjust the database. Generally it happens during major and minor version changes. Meaning that upgrade from 1.1.5 to 1.2.2 will probably require a migration, but 1.1.5 to 1.1.9 will not. If upgrading several minor version you'll need to apply all database migrations sequentially.

---

## Upgrading to 1.6.11+
Discovered a crappy paperclip default that now corrected with `config.upload_file_options`. Now default attachment `url` is set to `/system/:class/:id/:attachment/:style/:filename` instead of `/system/:attachment/:id/:style/:filename`. This means you'll need to move directories to adjust for this change. Not a problem if you never uploaded any files through CMS, or have your own override in place.

## Upgrading from 1.5.x to 1.6.0
* Replaced Wymeditor with elRTE.
* Integrated image insertion with uploaded files.
* Categories are scoped on Sites.
* Cleaned up mess with slugs/labels. Now if your `find_by_slug` method is failing you want to replace it with `find_by_identifier`. Sites have identifiers now too.
* Bumped up paperclip version in the Gemfile. Anything above 2.3.0 is OK. Choose your version wisely.
* Migration file: [[https://raw.github.com/comfy/comfortable-mexican-sofa/master/db/upgrade_migrations/07_upgrade_to_1_6_0.rb]]
* Don't forget to `rails g comfy:cms` if not using asset pipeline.
* You also might need to refresh thumbnails for previously uploaded images with: `rake paperclip:refresh CLASS=Cms::File`

## Upgrading from 1.4.x to 1.5.0
* Introducing Collection and PageFile(s) tags.
* Reordering functionality for Layouts, Snippets and Files.
* As always migration is needed: [[https://raw.github.com/comfy/comfortable-mexican-sofa/master/db/upgrade_migrations/06_upgrade_to_1_5_0.rb]]
* Rails 3.0 users please run `rails g comfy:cms` to refresh CSS.

## Upgrading from 1.3.x to 1.4.0
* You can manage your uploads from the dedicated Files section. It will even allow you to upload multiple files at the same time.
* Pages, snippets and files can be categorized. Helps with management and allows you to pull collections like this: `@site.files.for_category('red_category', 'blue_category')`
* Don't forget to apply the migration [[https://github.com/comfy/comfortable-mexican-sofa/raw/master/db/upgrade_migrations/05_upgrade_to_1_4_0.rb]]
* There are some CSS and JS changes as well, so run `rails g comfy:cms` if running Rails 3.0

## Upgrading from 1.2.x to 1.3.0
* Multiple Sites is a default functionality now. Setting to toggle it in the initializer is gone. `content_prefix_path` is an attribute of the Site now. This way if you want to serve pages from `http://localhost/en/` you need to set up a Site with **hostname** `localhost` and **path** `en`.
* Migration file can be found here: [[https://github.com/comfy/comfortable-mexican-sofa/raw/master/db/upgrade_migrations/04_upgrade_to_1_3_0.rb]]
* Page caching (along with the initializer setting) is removed for the time being as it doesn't work for multiple sites.

## Upgrading from 1.1.x to 1.2.0
* Revision system is introduced and that's why you need to grab this migration: [[https://github.com/comfy/comfortable-mexican-sofa/raw/master/db/upgrade_migrations/03_upgrade_to_1_2_0.rb]]. Just create a new migration, paste content of the above file and `rake db:migrate`.
* New initializer setting is added `revisions_limit`: [[https://github.com/comfy/comfortable-mexican-sofa/raw/master/config/initializers/comfortable_mexican_sofa.rb]]

## Upgrading from 1.0.x to 1.1.1
* There was slight reorganization of internals so there's a quick migration to make everything work again: [[https://raw.github.com/comfy/comfortable-mexican-sofa/master/db/upgrade_migrations/02_upgrade_to_1_1_0.rb]]. Just create a new migration, paste content of the above file and `rake db:migrate`.
* Some initializer settings got changed/removed. See: [[https://github.com/comfy/comfortable-mexican-sofa/raw/master/config/initializers/comfortable_mexican_sofa.rb]]
* `CmsSite`, `CmsLayout`, `CmsPage`, `CmsSnippet` are changed to `Cms::Site`, `Cms::Layout`, `Cms::Page` and `Cms::Snippet`. It only matters if you directly manipulate those objects somehow.
