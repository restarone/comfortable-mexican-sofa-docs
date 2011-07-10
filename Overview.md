Content creation in ComfortableMexicanSofa happens in 3 stages:

### Layout Creation
Layout defines the structure of the page. Here's a simple example of one:

    <html>
      <body>
        <h1>{{cms:page:title:string}}</h1>
        <div class="left_column">
          {{cms:page:left_column}}
        <div class="right_column">
          {{cms:page:right_column}}
        </div>
        <div class="footer">{{cms:snippet:footer}}</div>
      </body>
    </html>

Here we have one 3 page elements that we can manage: `title`, `left_column` and `right_column`, and one snippet element: `footer`.

### Page Creation
Based on the page tags defined in the Layout during page creation you'll see 3 corresponding form fields. Snippets are managed in their own section. Populate the content and save the page.

You may always return back to layout editing and add/remove tags. Page management view will adjust based on what tags you have defined in the layout.

### Page rendering
After page is created you can view it. Based on the example above the output should look like this:

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

All tags are always replaced with corresponding content.

This simple mechanism allows you to control all aspects of page structure and presentation.

  
