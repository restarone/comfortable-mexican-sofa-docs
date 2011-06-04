# ComfortableMexicanSofa (MicroCMS)

ComfortableMexicanSofa's content management is simple, yet incredibly flexible. Here's how it's done:

<table>
  <tr>
    <th>CMS Layout</th>
    <th>Cms Page Creation</th>
    <th>Final Result</th>
  </tr>
  <tr>
    <td>
      <pre>
&lt;html&gt;
  {{ cms:page:header }}
  {{ cms:page:body }}
  {{ cms:page:footer }}
&lt;/html&gt;
      </pre>
    </td>
    <td>
      <pre>
[ form field for header ]
[ form field for body   ]
[ form field for footer ]
      </pre>
    </td>
    <td>
      <pre>
&lt;html&gt;
  header content
  body content
  footer content
&lt;/html&gt;
      </pre>
    </td>
  </tr>
</table>
    
**Step 1:** First, a Layout is created. There you define your HTML structure for the page and tags that are used to populate content.<br/>
**Step 2:** Tags that were defined in the Layout dictate what form fields are going to be rendered during Page creation.<br/>
**Step 3:** When rendering a Page, Layout content and Page content (along with everything else) are merged and displayed.

* **Tags: [[Page Tag]]**
* **Tags: [[Field Tag]]**
* **Tags: [[Snippet Tag]]**
* **Tags: [[Helper and Partial Tags]]**
* **Tags: [[Upload Tags]]**
* **Tags: [[Asset Tags]]**
* **Layouts: [[Using Application Layout]]**
* **Layouts: [[Nesting Layouts]]**
* **Layouts: [[CMS managed CSS and JS]]**
* **[[Sites]]**

### Using CMS from your Application
* **[[View Rendering]]**
* **[[Using CMS Instance Variables]]**
* **[[View Helpers]]**

### Extending Admin Area
* **[[ViewHooks]]**

### CMS Fixtures
* **[[Working with CMS fixtures]]**

### Upgrading from a previous version ###
To upgrade to a newer version of Sofa you must bump up the version number in your Gemfile and run `bundle install`. After that run `rails g cms` and if necessary replace css/js/images with newer versions. Sometimes there will be migrations that you'll need to run. They will be found in [/db/migrate/upgrades](https://github.com/twg/comfortable-mexican-sofa/tree/master/db/migrate/upgrades). You'll need to run them in sequence starting with whatever version you're upgrading from.

* **[[Upgrading from 1.0.x to 1.1.1]]**
* **[[Upgrading from 1.1.x to 1.2.0]]**

### Contact
You if you have any questions feel free to contact me via [GitHub](https://github.com/gbh) or [@GroceryBagHead](http://twitter.com/#!/GroceryBagHead)