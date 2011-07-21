Snippets are reusable pieces of content that you'd want to manage from Sofa. Things like copyright notices, maybe even more complex things like navigations. When you create a snippet you need to provide a unique slug. For our example we'll use 'copyright'. Then we can use this snippet in our layout like so:

    <html>
      <body>
        {{ cms:page:content }}
        <div class='footer'>
          {{ cms:snippet:copyright }}
        </div>
      </body>
    </html>
    
If you ever need to access snippet content from inside your app you can use this helper: `cms_snippet_content(snippet_slug, cms_site = nil)`