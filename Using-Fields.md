Here is an example of using a field to add meta information to pages.

1. Inside of a Rails layout (e.g. app/views/application.html.erb) add a meta tag to the head content of the page:

  ```html
    <meta name="description" content="<%= cms_block_content(:meta_description) %>">
  ```

  Where `:meta_description` is the label for the content that you will add.

2. Inside of the Comfy CMS layout add a field:

  ```html
  {{ cms:field:meta_description:string }}
  ```

  This field includes the label (meta_description) and the type of content (string).

3. Inside of a page using the above layout, you will now see a text input that you can fill in with your string content.

4. The new field will have the label "Meta Description". If you want to change this, you need to add a localisation. Below example translates the label for meta_description into German (config/locales/de.comfy.yml): 
  ```
  de:
    activerecord:
      attributes:
        comfy/cms/page:
          meta_description: "Kurzbeschreibung"