# Comfortable Mexican Sofa
A more detailed explanation of functionality outlined in [README](https://github.com/twg/comfortable-mexican-sofa#readme)

### Managing Content
ComfortableMexicanSofa's content management is simple, yet incredibly flexible. Here's how it's done:

* First, a Layout is created. There you define your HTML structure for the page and tags that are used to populate content.
* Tags that were defined in the Layout dictate what form fields are going to be rendered during Page creation.
* When rendering a Page, Layout content and Page content (along with everything else) are merged and displayed.

This way you have a freedom to define page structure in any way you want.
    
    CMS Layout                          CMS Page Creation                   Final Result
    ╔═══════════════════════════╗       ╔═══════════════════════════╗       ╔═══════════════════════════╗
    ║  <html>                   ║       ║                           ║       ║  <html>                   ║
    ║    {{cms:page:header }}   ║       ║ [ form field for header ] ║       ║    header content         ║
    ║    {{cms:page:body }}     ║  ==>  ║ [ form field for body   ] ║  ==>  ║    body content           ║
    ║    {{cms:page:footer }}   ║       ║ [ form field for footer ] ║       ║    footer content         ║
    ║  </html>                  ║       ║                           ║       ║  </html>                  ║
    ╚═══════════════════════════╝       ╚═══════════════════════════╝       ╚═══════════════════════════╝

* **[[Tags: Page]]**
* **[[Tags: Field]]**
* **[[Tags: Snippet]]**
* **[[Tags: Helper and Partial]]**
* **[[Layouts: Using Application Layout]]**
* **[[Layouts: Nesting Layouts]]**
* **[[Layouts: CMS managed CSS and JS]]**
* **[[Sites]]**

### Using CMS from your Application
* **[[View Rendering]]**
* **[[Accessing CmsPage content directly]]**

### Extending Admin Area
* **[[ViewHooks]]**

### CMS Seeds
* **[[Working with CMS seeds]]**

### Extras
* [Why ComfortableMexicanSofa? What's with the name?](http://blog.twg.ca/2011/02/the-comfortable-mexican-sofa-vitamin-d-infused/)