# Nesting Layouts

Let's say you need to define a CMS Layout that has left and right columns. It looks exactly like your one-column layout, but now there's two. You *could* just copy-paste it and modify it, but that's not really good. Remember the often-used `{{ cms:page:content }}` tag? Page tags with `content` label allow layout nesting. 

Here's a scenario when Layout B is a child of Layout A

    CMS Layout A                        CMS Layout B                        CMS Page Creation
    ╔═══════════════════════════╗       ╔═══════════════════════════╗       ╔═══════════════════════════╗
    ║  <html>                   ║       ║ <div class='left'>        ║       ║ [ form field for header ] ║
    ║    {{cms:page:header }}   ║       ║   {{cms:page:left}}       ║       ║ [ form field for left   ] ║
    ║    {{cms:page:content }}  ║  ==>  ║ </div><div class='right'> ║  ==>  ║ [ form field for right  ] ║
    ║    {{cms:page:footer }}   ║       ║   {{cms:page:right}}      ║       ║ [ form field for footer ] ║
    ║  </html>                  ║       ║ </div>                    ║       ║                           ║
    ╚═══════════════════════════╝       ╚═══════════════════════════╝       ╚═══════════════════════════╝

Notice that `{{ cms:page:content }}` is substituted with tag definitions from Layout B. This is really all there's to it.