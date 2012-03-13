Sitemaps are automatically generated for your site at /sitemap.xml. 

To extend a sitemap, you can register callbacks that will be invoked when a sitemap is requested. 

For example, registering a callback which will add SiteNews to the sitemap would look like the following
<pre>
ComfortableMexicanSofa::Sitemap.register_extension(
  SiteNews.method(:sitemap_callback))
</pre>

The callback is passed the current cms_site, an instance of the view being rendered, and an instance of the xmlbuilder being used to construct the sitemap. 

This allows the following to work, which would add the site news to the sitemap:

<pre>
class SiteNews &lt; ActiveRecord::Base
  def self.sitemap_callback(cms_site, view, xml)
    scoped.where(:cms_site_id =&gt; cms_site).published.each do |news|
      xml.url do
        xml.loc view.site_news_url(news)
        xml.lastmod news.updated_at.strftime('%Y-%m-%d')
      end
    end
  end
end
</pre>