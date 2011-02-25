# CMS Managed CSS and JS

Sofa gives you ability to manage CSS and JS for each Layout. This functionality is generally useful if you decide not to use application layouts.

You access CSS via this URL: `http://yoursite.local/cms-css/*layout-slug*.css`. Similarly for JS: `http://yoursite.local/cms-css/*layout-slug*.js`

Here's an example for Layout with `default-layout` slug:

    <!DOCTYPE html>
    <html>
      <head>
        <link href="/cms-css/default-layout.css" media="screen" rel="stylesheet" type="text/css" />
        <script src="/cms-js/default-layout.js" type="text/javascript"></script>
      </head>
      <body>
        {{ cms:page:content }}
      </body>
    </html>
    
You can access CSS/JS for any Layout from anywhere. So technically, you can have CMS managed CSS/JS for your entire application.