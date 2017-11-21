## Content Tags

TODO

### Content Tag Namespaces

You can organize your page fragments into tabbed sections by passing `namespace`
parameter. If you wanted to organize a set of Open Graph fields into an "Og"
tab, your layout might look something like this:

```html
    {{ cms:text title }}
    {{ cms:text description }}
    ...
    {{ cms:text open_graph_description, namespace: OG }}
    {{ cms:text open_graph_title, namespace: OG }}
```

Comfy will create two tabs in the page editor: Default and OG. The `title` and
`description` fields will be displayed in the Default tab and the two namespaced
fields will be displayed in the OG tab.
