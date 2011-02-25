# Helper and Partial Tags

By default, Sofa doesn't allow you to use ERB when populating content. This is done to prevent accidental (or malicious) code execution that might destroy database content. However, to provide content that comes from your application you need a way to provide access to helper methods and partials.

### Helper Tags

To provide access to helpers you have Helper tags available to you:

    {{ cms:helper:method_name }}
    
this is equivalent to:

    <%= method_name %>
    
If you need to provide additional parameters it's done like so:

    {{ cms:helper:method_name:x:y:z }}
    
this is equivalent to:
    
    <%= method_name('x', 'y', 'z') %>
    
If you don't have that helper available an exception will be thrown.

### Partial Tags

Same idea as for helpers, here's a tag that allows access to your partials:
    
    {{ cms:partial:path/to/partial }}
    
this is equivalent to:
    
    <%= render :partial => 'path/to/partial' %>
    
With additional parameters:
    
    {{ cms:partial:path/to/partial:a:b }}
    
same as:
    
    <%= render :partial => 'path/to/partial', :locals => { :param_1 => 'a', :param_2 => 'b' } %>
    
You cannot really name those parameters, so you'd want to do some translation to make your partial readable (but that's up to you).
    