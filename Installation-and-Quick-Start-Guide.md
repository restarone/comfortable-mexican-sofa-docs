### Installation
Add the gem definition to your Rails project's Gemfile:
    
    gem 'comfortable_mexican_sofa'
    
Then from your Rails project's root run these commands:
    
    bundle install
    rails generate comfy:cms
    rake db:migrate

The generator will create the initializer, database migration, example CMS fixtures, and, if running Rails 3.0, will copy all necessary assets into `/public` directory.

If you are upgrading from an older version of ComfortableMexicanSofa, please take a look at [[Upgrading ComfortableMexicanSofa]]

### Quick Start Guide
After finishing installation you should be able to navigate to http://yoursite/cms-admin

The default username and password after installation is 'username' and 'password', which you will probably want to change right away. You can do so by editing the admin credentials, which can be found and changed in the cms initializer: [/config/initializers/comfortable\_mexican\_sofa.rb](https://github.com/comfy/comfortable-mexican-sofa/blob/master/config/initializers/comfortable_mexican_sofa.rb)

    ComfortableMexicanSofa::HttpAuth.username = 'username'
    ComfortableMexicanSofa::HttpAuth.password = 'password'

Before we can populate the site with content, we will need to create a Site. The Site is what defines the hostname, content path, and the language. After creating a Site, you need to make a Layout, which is the template for your content; allowing you to define reusable content (such as the header and footer) and placeholders for content.

A very simple Layout can look like this:
    
    <html>
      <body>
        <h1>{{ cms:page:header:string }}</h1>
        {{ cms:page:content:text }}
      </body>
    </html>

Once you have a Layout, you can create Pages, where the content is populated for your Layouts. It's that easy. Hint: if the system cannot find any content tags in the chosen layout when using 1.9,3,p327 -> downgrade to 1.9,3,p125 and it will work.