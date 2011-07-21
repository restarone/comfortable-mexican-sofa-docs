Layout defines content areas for the page. For example, if you need a page with header, footer, and some content you'd need something like this:

    <html>
      <body>
        <div class='header'>
          {{ cms:snippet:header }}
        </div>
        <div class='content'>
          <h1> {{ cms:page:title:string }} </h1>
          {{ cms:page:content }}
        </div>
        <div class='footer'>
          {{ cms:snippet:footer }}
        </div>
      </body>
    <html>
    
If this layout is chosen during page creation you will notice that you are presented with form fields that correspond to the tags defined in the layout content. In this case you'll have a _Title_ text field and _Content_ text area. When page is rendered, tags are replaced with content that you defined.

### Application Layout
In most cases you'll want to use stylesheets/javascripts and general html layout that you already have in your application. For that it's enough to select an `App Layout`. It will be listed as a file that is found in `/views/layouts`. This way you limit exposure of what can be managed in Sofa. Let's say your application layout is `application.html.haml`:

    !!! html
    %html
      %head
        = render :partial => 'layouts/head'
      %body
        = render :partial => 'layouts/header'
        .content
          = yield
        = render :partial => 'layout/footer'
    
Now we don't need to worry about anything but the left and right columns. We can simplify our layout to:
    
    <h1> {{ cms:page:title:string }} </h1>
    {{ cms:page:content }}

### Nested Layouts
Let's say you need to define a CMS Layout that has left and right columns. It looks exactly like your one-column layout, but now there's two. You could just copy-paste it and modify it, but that's not really good. Remember the often-used {{ cms:page:content }} tag? Page tags with _content_ label allow layout nesting.

Based on the previous examples this is what two-column layout would look like:
  
    <div class='left'> {{ cms:page:left_column }} </div>
    <div class='right'> {{ cms:page:right_column }} </div>
  
But what about the _Title_? If you specify our first layout as a parent in actuality you are dealing with layout that has this content:

    <h1> {{ cms:page:title:string }} </h1>
    <div class='left'> {{ cms:page:left_column }} </div>
    <div class='right'> {{ cms:page:right_column }} </div>
  
What happened here is that content of this layout is merged into the parent via `{{ cms:page:content }}` tag. You can have multiple levels of nesting if you so desire.

### CSS and JS
You can manage CSS right here in Sofa. Helps in those cases when you need to move that logo 2px to the left without redeploying the application. The trick is to somehow link that resource to the page. You'll notice that you have routes available:
    
    cms_css GET    /cms-css/:site_id/:layout_slug(.:format) {:controller=>"cms_content", :action=>"render_css"}
    cms_js  GET    /cms-js/:site_id/:layout_slug(.:format)  {:controller=>"cms_content", :action=>"render_js"}
    
So all you need to do is link to a proper path. So if your site has _id_ `1` and layout slug is `default` the path to css will be: `/cms-css/1/default.css`. Same applies to javascript link.

If you fully manage layouts you can use a tag to link to css/js:

    <html>
      <head>
        {{ cms:asset:default:css:html_tag }}
        {{ cms:asset:default:js:html_tag }}
      </head>
    </html>
    
If you use application layout this is how you'd access assets:
  
    <%= stylesheet_link_tag cms_css_path(@cms_site.id, @cms_layout.slug) %>
    <%= javascript_include_tag cms_js_path(@cms_site.id, @cms_layout.slug) %>
