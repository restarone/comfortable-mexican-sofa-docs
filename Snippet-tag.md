# Snippet Tag

Snippets are created in /cms-admin/snippets area and their content can be used inside Layouts, Pages and even other Snippets via snippet tags. Snippets have unique identifier, or `slug`. This slug is used in tag definitions.

    CMS Layout                            CMS Page Creation                   Final Result
    ╔═════════════════════════════╗       ╔═══════════════════════════╗       ╔═══════════════════════════╗
    ║  <html>                     ║       ║                           ║       ║  <html>                   ║
    ║    {{cms:page:body}}        ║       ║ [ form field for body ]   ║       ║    body content           ║
    ║    {{cms:snippet:AAA}}      ║  ==>  ║                           ║  ==>  ║    AAA snippet content    ║
    ║  </html>                    ║       ║                           ║       ║  </html>                  ║
    ╚═════════════════════════════╝       ╚═══════════════════════════╝       ╚═══════════════════════════╝
    
Now, let's assume that our CMS Page content has `{{cms:snippet:BBB}}` and content of AAA snippet defines `{{cms:snippet:CCC}}`. Our final output will look something like this:

    <html>
      body content with BBB snippet content
      AAA snippet content with CCC snippet content
    </html>
    
If you never created snippet with defined slug, nothing will be rendered in place of that snippet.