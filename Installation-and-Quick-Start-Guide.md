### Installation
Add gem definition to your Gemfile:
    
    gem 'comfortable_mexican_sofa'
    
Then from the Rails project's root run:
    
    bundle install
    rails generate cms
    rake db:migrate

Generator will create the initializer, database migration, example cms fixtures, and if running Rails 3.0 will copy all necessary assets into /public directory.

When upgrading from the older version please take a look at [[Upgrading ComfortableMexicanSofa]]

### Quick Start Guide
After finishing installation you should be able to navigate to http://yoursite/cms-admin

Default username and password is 'username' and 'password'. You probably want to change it right away. Admin credentials (among other things) can be found and changed in the cms initializer: [/config/initializers/comfortable\_mexican\_sofa.rb](https://github.com/twg/comfortable-mexican-sofa/blob/master/config/initializers/comfortable_mexican_sofa.rb)

Before creating pages and populating them with content we need to create a Site. Site defines a hostname, content path and it's language.

After creating a Site, you need to make a Layout. Layout is the template of your pages; it defines some reusable content (like header and footer, for example) and places where the content goes. A very simple layout can look like this:
    
    <html>
      <body>
        <h1>{{ cms:page:header:string }}</h1>
        {{ cms:page:content:text }}
      </body>
    </html>

Once you have a layout, you may start creating pages and populating content. It's that easy.