* Revision system is introduced and that's why you need to grab a migration: [[https://github.com/twg/comfortable-mexican-sofa/raw/master/db/migrate/upgrades/03_upgrade_to_1_2_0.rb]]. Just create a new migration, paste content of the above file and `rake db:migrate`.
* New initializer setting is added `revisions_limit`: [[https://github.com/twg/comfortable-mexican-sofa/raw/master/config/initializers/comfortable_mexican_sofa.rb]]

**Don't forget to run `rails g cms` to create/update css, js and images that Sofa uses.**
