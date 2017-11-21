## Overview

Sofa allows you to build your entire site using files instead of updating the
database via the admin area. This significantly speeds up initial content
population. Go to the initializer and set this to enable seeds in development
environment: `config.enable_seeds = Rails.env.development?`. You may also change
the folder that is used to store seeds by changing `config.seeds_path`, which
defaults to '/db/cms_seeds'.

If you run `rails g comfy:cms` you should find an example set of seeds in
[/db/cms\_seeds](https://github.com/comfy/comfortable-mexican-sofa/tree/master/db/cms_seeds).

When seeds are enabled, the database is updated with each request, but only if
seed file is newer than the database entry. Database is also purged of items that
are not defined in seeds. So be careful not to clear out your database by mistake.

### Importing into Database

To load seeds into the database just run this rake task:

```
rake 'comfy:cms_seeds:import[folder-name, site-identifier]'
```

First argument indicates folder seeds are in and second is the Site identifier
you have defined in the database.

### Exporting into Files

If you need to dump database contents into seed files run:

```
rake 'comfy:cms_seeds:export[site-identifier, folder-name]'
```

This will create folder-name folder in the directory defined by
`config.fixtures_path` and dump all content from site-identifier Site.

### Using CMS Seeds in tests

All you need to do is create a rake task like this:

```ruby
namespace :test do
  task :prepare do
    Comfy::Cms::Site.create!(identifier: 'site-identifier', hostname: 'localhost')
    Rake::Task['comfy:cms_seeds:import[folder-name, site-identifier]'].invoke
  end
end
```

Now, when runnining `rake` or `rake:test` CMS seeds will be loaded in.
