* There was slight reorganization of internals so there's a quick migration to make everything work again: [[https://github.com/twg/comfortable-mexican-sofa/raw/fixtures/db/migrate/upgrades/02_upgrade_to_1_1_0.rb]]
* Some initializer settings got changed/removed: [[https://github.com/twg/comfortable-mexican-sofa/raw/master/config/initializers/comfortable_mexican_sofa.rb]]
* `CmsSite`, `CmsLayout`, `CmsPage`, `CmsSnippet` are changed to `Cms::Site`, `Cms::Layout`, `Cms::Page` and `Cms::Snippet`. It only matters if you directly manipulate those objects somehow.
