# Using Application Layout

Instead of redefining all the structural html/css in Layouts you can use your layouts you already have in your application. Imagine your application.erb.html looks like this:

    <!DOCTYPE html>
    <html>
      <head>
        <title>My Awesome Application</title>
        <%= stylesheet_link_tag :default %>
        <%= javascript_include_tag :default %>
      </head>
      <body>
        <%= render :partial => 'main_navigation' %>
        <%= yield %>
        <%= render :partial => 'footer' %>
      </body>
    <html>
    
That's a lot of markup we don't really want to duplicate into CMS. You can simply use **App Layout** dropdown during CMS Layout creation/editing. Now everything that CMS renders will be output into the `yield` of the selected application layout. This way your CMS layouts can be light and easy to manage. However, now you have no access to structural html and css, but that can be a *good* thing.