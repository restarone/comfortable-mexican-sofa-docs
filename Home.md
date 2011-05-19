# ComfortableMexicanSofa (MicroCMS)

### Managing Content
ComfortableMexicanSofa's content management is simple, yet incredibly flexible. Here's how it's done:
    
    CMS Layout                          CMS Page Creation                   Final Result
    ╔═══════════════════════════╗       ╔═══════════════════════════╗       ╔═══════════════════════════╗
    ║  <html>                   ║       ║                           ║       ║  <html>                   ║
    ║    {{cms:page:header }}   ║       ║ [ form field for header ] ║       ║    header content         ║
    ║    {{cms:page:body }}     ║  ==>  ║ [ form field for body   ] ║  ==>  ║    body content           ║
    ║    {{cms:page:footer }}   ║       ║ [ form field for footer ] ║       ║    footer content         ║
    ║  </html>                  ║       ║                           ║       ║  </html>                  ║
    ╚═══════════════════════════╝       ╚═══════════════════════════╝       ╚═══════════════════════════╝
    
**Step 1:** First, a Layout is created. There you define your HTML structure for the page and tags that are used to populate content.<br/>
**Step 2:** Tags that were defined in the Layout dictate what form fields are going to be rendered during Page creation.<br/>
**Step 3:** When rendering a Page, Layout content and Page content (along with everything else) are merged and displayed.

* **Tags: [[Page Tag]]**
* **Tags: [[Field Tag]]**
* **Tags: [[Snippet Tag]]**
* **Tags: [[Helper and Partial Tags]]**
* **Layouts: [[Using Application Layout]]**
* **Layouts: [[Nesting Layouts]]**
* **Layouts: [[CMS managed CSS and JS]]**
* **[[Sites]]**

### Using CMS from your Application
* **[[View Rendering]]**
* **[[Using CMS Instance Variables]]**
* **[[View Helpers]]**

### Extending Admin Area
* **[[ViewHooks]]**

### CMS Fixtures
* **[[Working with CMS fixtures]]**

### Upgrading from a previous version ###
To upgrade to a newer version of Sofa bust bump up the version number in your Gemfile and run `bundle install`. After that run `rails g cms` and if necessary replace css/js/images with newer versions. Sometimes there will be migrations that you'll need to run. They will be found in [/db/migrate/upgrades](https://github.com/twg/comfortable-mexican-sofa/tree/master/db/migrate/upgrades). You'll need to run them in sequence starting with whatever version you're upgrading from.

* **[[Upgrading from 1.0.x to 1.1.1]]**
* **[[Upgrading from 1.1.x to 1.2.0]]**

### Roadmap and Coming Features
1. Finalizing Mirrored sites functionality
2. Implementing 'Shared' resources. Layouts/Pages/Snippets that are exactly the same across all Sites. Will ride on top of Mirrored functionality.
3. Replacing tinyMce with wymeditor (very likely)
4. Figuring out i18n for mirror sites and hostname/[en|fr|jp]. Maybe Site can be defined as hostname + locale path prefix.
5. Making Uploads more useful. Integration with wysiswyg editor and making side widget less useless.
6. Adjusting Fixtures functionality to do both import and export. Better rake tasks.
7. Taking a look at page caching. Currently it plainly doesn't work with multiple sites.
8. Moving images/css/js to app/assets. I guess going Sass way will make it possible to serve css in both Rails 3.1 and 3.0 directly from the engine without moving things to public? Would be nice to get it working before RC gets released.

### Contact
You if you have any questions feel free to contact me via [GitHub](https://github.com/gbh) or [@GroceryBagHead](http://twitter.com/#!/GroceryBagHead)