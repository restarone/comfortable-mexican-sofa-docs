You can setup ComfortableMexicanSofa so it serves content from a different database than your application. This can be accomplished via changing this setting in the initializer:

    config.database_config = 'custom'

Now you need to create definition in your `database.yml` file for `custom_development` and `custom_production`, and other environments you may have. 

#### Things to keep in mind:
- Note that in `test` environment it will use only same database as your main app for testing. That's just what Rails does.
- You'll need to edit migrations to include `ComfortableMexicanSofa.establish_connection(ActiveRecord::Base)` so they are run using proper database configuration.
- the line abowe is crap (for v. 1.11.2), the feature may be useful, but only for a legacy database, maitained only via cms panel, plus it will spawn a db connection for each model