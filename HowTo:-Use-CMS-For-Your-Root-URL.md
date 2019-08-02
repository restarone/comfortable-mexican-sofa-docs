By default, Comfy will map the root url of your web site, but you can't use "root_url" in your controllers or helpers.  Since that's a popular destination for redirects, it might be desirable to be able to use "root_url".

Add this line at the top of your routes:

    root controller: 'comfy/cms/content', cms_path: '', action: 'show'

You can then use `root_url` and `root_path`, as well as `:root` normally now, and still make use of what CMS has to offer.