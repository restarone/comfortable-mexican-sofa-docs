Sofa allows you to build entire site using files instead of updating database via admin area. This significantly speeds up initial content population. Go to the initializer and set this to enable fixtures in development environment: `config.enable_fixtures = Rails.env.development?`. You may also change the folder that is used to store fixtures.

If you run `rails generate cms` you should find an example set of fixtures in [/db/cms\_fixtures](https://github.com/comfy/comfortable-mexican-sofa/tree/master/db/cms_fixtures).

When fixtures are enabled, the database is updated with each request, but only if fixture file is newer than the database entry. Database is also purged of items that are not defined in fixtures. So be careful not to clear out your database by mistake.

### Importing into Database
To load fixtures into the database just run this rake task: `rake comfortable_mexican_sofa:fixtures:import FROM=folder-name TO=site-identifier`. `from` indicates folder the fixtures are in and `to` is the Site identifier you have defined in the database.

### Exporting into Files
If you need to dump database contents into fixture files run: `rake comfortable_mexican_sofa:fixtures:export FROM=site-identifier TO=folder-name`. This will create forder-name folder and dump all content from example.com Site.

### Using Fixtures in tests
All you need to do is create a rake task like this:
    
    namespace :test do
      task :prepare do
        ENV['FROM'] = 'folder-name'
        ENV['TO']   = 'site-identifier'
        Rake::Task['comfortable_mexican_sofa:fixtures:import'].invoke
      end
    end

Now, when runnining `rake` or `rake:test` CMS fixtures will be loaded in.