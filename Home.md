# Comfortable Mexican Sofa
A more detailed explanation of functionality outlined in [README](https://github.com/twg/comfortable-mexican-sofa#readme)

** Please feel free to edit with Wiki **

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

### CMS Seeds
* **[[Working with CMS seeds]]**

### Upgrading from a previous version ###
To upgrade to a newer version of Sofa bust bump up the version number in your Gemfile and run `bundle install`. After that run `rails g cms` and if necessary replace css/js/images with newer versions. Sometimes there will be migrations that you'll need to run. They will be found in (/db/migrate/upgrades/)[https://github.com/twg/comfortable-mexican-sofa/tree/master/db/migrate/upgrades]. You'll need to run them in sequence starting with whatever version you're upgrading from.
* **[[Upgrading from 1.0.x to 1.1.1]]**

### Extras
* [Why ComfortableMexicanSofa? What's with the name?](http://blog.twg.ca/2011/02/the-comfortable-mexican-sofa-vitamin-d-infused/)