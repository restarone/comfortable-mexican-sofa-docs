Sofa allows you to override the default buttons that appear on the JS rich_text/WYSIWYG editor. For more information on the available buttons and panels, visit http://elrte.org/redmine/projects/elrte/wiki/Docs_EN#Custom-toolbar

Use [ViewHooks][[Reusing sofa's admin area]] to link up a JS file in Sofa's Head with the following:

`$.CMS.cms_config['elRTE']['toolbar'] = [];` 

Fill the blank array with the items you'd like in the toolbar. 

For example, to use HTML table controls, you'd specify:

`$.CMS.cms_config['elRTE']['toolbar'] = ['tables'];`