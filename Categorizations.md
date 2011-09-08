Pages, Snippets and Files can be categorized. It allows for easier organization and also allows easier access to from your application.

For example, on the homepage we have some sort of a carousel element with a number of slides that client wants to manage. We don't trust that client enough not to horribly mess up the HTML, so we going to use Snippets to solve this problem. All we need to do is assign snippets to category `carousel` and then from your application we can easily access them like so:

    - Cms::Snippet.of_type('carousel').each do |slide|
      .slide= slide.content

If you have multiple sites going on you'll need to make sure that you're not pulling content from a wrong site:

    - @cms_site.snippets.of_type('carousel')