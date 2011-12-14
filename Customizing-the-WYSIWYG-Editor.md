Sofa allows you to override the default buttons that appear on the JS rich_text/WYSIWYG editor. For more information on the available buttons and panels, visit http://elrte.org/redmine/projects/elrte/wiki/Docs_EN#Custom-toolbar

Simply add the following to your JS: 

`$.CMS.cms_config['elRTE']['toolbar'] = [];` 

Fill the blank array with the items you'd like in the toolbar. 

For example, to use the default CMS buttons as well as HTML table controls, you'd specify:

`$.CMS.cms_config['elRTE']['toolbar'] = ['undoredo', 'sofa_format', 'sofa_style', 'sofa_alignment', 'lists', 'sofa_copypaste', 'sofa_links', 'sofa_image', 'tables'];`