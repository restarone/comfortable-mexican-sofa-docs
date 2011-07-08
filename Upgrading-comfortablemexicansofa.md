To upgrade to a newer version of Sofa you must bump up the version number in your Gemfile and run `bundle install`. After that run `rails g cms` and if necessary replace css/js/images with newer versions. Sometimes there will be migrations that you'll need to run. They will be found in [/db/migrate/upgrades](https://github.com/twg/comfortable-mexican-sofa/tree/master/db/migrate/upgrades). You'll need to run them in sequence starting with whatever version you're upgrading from.

* **[[Upgrading from 1.0.x to 1.1.1]]**
* **[[Upgrading from 1.1.x to 1.2.0]]**