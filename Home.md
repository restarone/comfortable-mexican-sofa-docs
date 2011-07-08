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

#### [Working with CMS fixtures][fixtures]
#### [Upgrading ComfortableMexicanSofa][upgrading]

### Contact
You if you have any questions feel free to contact me via [GitHub](https://github.com/gbh) or [@GroceryBagHead](http://twitter.com/#!/GroceryBagHead)