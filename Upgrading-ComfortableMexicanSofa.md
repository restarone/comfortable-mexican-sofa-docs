To upgrade to a newer version of ComfortableMexicanSofa you must bump up the version number in your Gemfile like so:

    gem 'comfortable_mexican_sofa', '~> 1.10.0'

and run `bundle install`. 

Sometimes you'll need to create migrations to adjust the database. Generally it happens during major and minor version changes. Meaning that upgrade from 1.1.5 to 1.2.2 will probably require a migration, but 1.1.5 to 1.1.9 will not. If upgrading several minor version you'll need to apply all database migrations sequentially.

To find the migrations go take a look at [comfortable-mexican-sofa/db/upgrade_migrations/](https://github.com/comfy/comfortable-mexican-sofa/tree/master/db/upgrade_migrations).
Just create a migration with the name in the file concerning you and copy the text over.

For list of releases and relevant notes please see: https://github.com/comfy/comfortable-mexican-sofa/releases