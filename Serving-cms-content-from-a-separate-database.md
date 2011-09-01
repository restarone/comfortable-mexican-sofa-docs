You can setup ComfortableMexicanSofa so it serves content from a different database than your application. This can be accomplished via changing this setting in the initializer:

    config.database_config = 'custom'

Now you need to create definition in your `database.yml` file for `custom_development` and `custom_production`, and other environments you may have. Note that in `test` environment it will use only same database as your main app for testing. That's just what Rails does.