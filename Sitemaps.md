Sitemaps are automatically generated for your site at /sitemap.xml. Output is based on the structure of the published pages.

Make sure that in `routes.rb` you have sitemap route enabled: `ComfortableMexicanSofa::Routing.content :sitemap => true`

If you want to modify what gets outputted feel free to overwrite view template file:
* Copy https://raw.github.com/comfy/comfortable-mexican-sofa/master/app/views/cms/content/render_sitemap.xml.builder
* Paste it into `app/views/cms/content/` folder inside your application
* Modify away