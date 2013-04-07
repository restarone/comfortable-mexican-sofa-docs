There are three stages of development when creating content in ComfortableMexicanSofa.

## Layout Creation
A Layout defines the structure of the page, allowing you to define reusable content (such as the header and footer) and placeholders for content.

Here's a simple example of one:
```html
<html>
  <body>
    <h1>{{cms:page:title:string}}</h1>
    <div class="left_column">
      {{cms:page:left_column}}
    </div>
    <div class="right_column">
      {{cms:page:right_column}}
    </div>
    <div class="footer">{{cms:snippet:footer}}</div>
  </body>
</html>
```

Here we have created three content placeholder elements, or tags, for a Page that allow us to manage content on the Page Creation side of things: `title`, `left_column` and `right_column`, and one snippet element: `footer`.

## Page Creation
Because of the Page placeholders defined when we created our example Layout above, when you create a Page that utilizes that Layout, you will see three corresponding fields to be populated with content. Snippets are managed separately from Page tags and have their own section. You can populate the fields with content and save the page.

You can always edit the Layout and add or remove Page tags. The Page editing view will adjust based on what tags you have defined in the Layout.

## Page Rendering
After a Page is created you can view the output. Based on the example above the output should look like this:

```html
<html>
  <body>
    <h1>Example Page Title</h1>
    <div class="left_column">
      Left Column Content
    <div class="right_column">
      Right Column Content
    </div>
    <div class="footer">Footer Content</div>
  </body>
</html>
```

All tags are populated with corresponding content from the Page editing view.

This simple mechanism allows you to control all aspects of page structure and presentation.