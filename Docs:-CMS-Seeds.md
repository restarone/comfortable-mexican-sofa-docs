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
    Rake::Task['comfy:cms_seeds:import'].invoke('folder-name', 'site-identifier')
  end
end
```

Now, when runnining `rake` or `rake:test` CMS seeds will be loaded in.

### Seed File Structure

#### For Layouts

Layout seed files live in this default folder: `/db/cms_seeds/site_identifier/layouts`.
Each Layout is denoted by the folder name and associated `content.html` file.
Nested layouts are just sub-folders. Here's an example of a layout seed and a nested one.

```text
layouts
  +-- default
  |  +-- nested
  |     +-- content.html
  +-- content.html
```

Here's an example of content.html structure. Lines with `[something]` indicate
file sections.

```html
[attributes]
label: Main Layout

[content]
<html>
  <body>
    {{ cms:wysiwyg content }}
  </body>
</html>

[js]
console.log("hello")

[css]
body{color: black}
```

#### For Pages

Page seed files located in this default folder: `/db/cms_seeds/site_identifier/pages`.
Each Page is denoted by folder name. Root page is named `index`. All other pages
are nested under that folder.

Translations are handled by files with locale in the filename: `cotnent.locale.html`.

Attachments are put on the same level as content file and linked from there.

```text
pages
  +-- index
  |  +-- child-a
  |  |  +-- content.html
  |  +-- child-b
  |     +-- content.html
  +-- content.html
  +-- content.fr.html
  +-- content.es.html
  +-- header.jpg
```

Here's an example content.html structure. Segments like `[type name]` maps to
a fragment type and name. For example, if you have `{{cms:markdown right-column}}`
you'll have `[markdown right-column]` section in content.html file.

```html
[attributes]
label: Homepage
layout: default
categories:
  - red
  - green

[file header]
header.jpg

[wysiwyg content]
Home Page content
{{ cms:snippet default }}

[date published_on]
2015-10-31
```

#### For Snippets

Snippet seed files located in `/db/cms_seeds/site_identifier/snippets`. Each
snippet is denoted by a file name like this: `snippet_identifier.html`

```text
snippets
  +-- footer.html
  +-- contact.html
```

Here's a simple example:

```html
[attributes]
label:Footer Snippet
categories:
  - blue
  - yellow

[content]
Copyright 2021
```

#### For Files

File seeds live in `/db/cms_seeds/site_identifier/files`. You can just dump
files in there as-is. If you need to add attributes like label, descriptions, etc
you need to add `_filename.extension.yml`

```text
files
  +-- header.jpg
  +-- footer.jpg
  +-- _footer.jpg.yml
```

Here's an example yml file:

```yml
label: Footer File
description: Footer File Description
categories:
  - purple
  - beige
```
