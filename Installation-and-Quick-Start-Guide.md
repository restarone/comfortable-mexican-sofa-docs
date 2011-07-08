Add gem definition to your Gemfile:
    
    gem 'comfortable_mexican_sofa'
    
Then from the Rails project's root run:
    
    bundle install
    rails generate cms
    rake db:migrate

Generator will create the initializer, database migration, example cms fixtures, and if running Rails 3.0 will copy all necessary assets into /public directory.

When upgrading from the older version please take a look at [[Upgrading ComfortableMexicanSofa]]