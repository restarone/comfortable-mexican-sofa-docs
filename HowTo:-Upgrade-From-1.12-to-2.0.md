Because of:

- Move from Paperclip to ActiveStorage
- Change of CMS tag structure
- Removal of Mirrored sites functionality and adding page translations

It's not that easy to upgrade 1.12 install to the current 2.0 version.

Here's a path that might work for you:

- In 1.12 install export all content to CMS Fixture files via `rake comfortable_mexican_sofa:fixtures:export FROM=site_identifier TO=folder_name`
- Remove existing 1.12 CMS related db tables and Paperclip attachment files wherever they might be.
- Edit files into new CMS Seeds format. [See Wiki entry on that](//github.com/comfy/comfortable-mexican-sofa/wiki/Docs:-CMS-Seeds).
- Change CMS tags from old `{{cms:foo:bar:red:green}}` format to the new `{{cms:foo bar, red: green}}`
- If you attached files via WYSIWYG editor prepare for the pain of trying to locate and re-link those files later.
- Install 2.0
- Import CMS Seeds with rake `comfy:cms_seeds:import[folder_name,site_identifier]`

Feel free to update this Wiki entry if you had to do this migration.
