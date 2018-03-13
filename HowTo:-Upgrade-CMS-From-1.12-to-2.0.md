Because of:

- Move from Paperclip to ActiveStorage
- Change of CMS tag structure
- Removal of Mirrored sites functionality and adding page translations

It's not that easy to upgrade 1.12 install to the current 2.0 version.

Here's a path that might work for you:

- In 1.12 install export all content to CMS Fixture files via `rake comfortable_mexican_sofa:fixtures:export FROM=site_identifier TO=folder_name`
- Remove existing 1.12 CMS related db tables and Paperclip attachment files wherever they might be.
- Edit files into new CMS Seeds format. [See Wiki entry on that](//github.com/comfy/comfortable-mexican-sofa/wiki/Docs:-CMS-Seeds).

  Begin by inlining all the `attributes.yml` files into `content.html` like this:

  ```ruby
  Dir['db/cms_seeds/**/content.html'].each do |path|
    attributes_path = File.join(File.dirname(path), 'attributes.yml')
    next unless File.readable?(attributes_path)
    attributes = File.read(attributes_path)
    attributes.sub!(/\A---\n/, '')
    attributes.sub!(/^parent: [^\n]+\n/, '')
    content = File.read(path)
    content_tag = path.include?('/pages'/) ? '[textarea content]' : '[content]'
    File.delete(attributes_path)
    if path.include? '/snippets/'
      File.delete(path)
      File.delete(File.dirname(path))
      path = path.sub('/content.html', '.html')
    end
    File.write(path, "[attributes]\n#{attributes}\n#{content_tag}\n#{content}")
  end
  ```

- Change CMS tags from old `{{cms:foo:bar:red:green}}` format to the new `{{cms:foo bar, red: green}}`.

  For most of these, you can do so using a few RegExps, such as:

  | Pattern | Replacement |
  |---------|-------------|
  | `\{\{ ?cms:helper:([\w]+) ?\}\}` | `{{ cms:helper $1 }}` |
  | `\{\{ ?cms:helper:([\w]+):([^:]*) ?\}\}` | `{{ cms:helper $1, "$2" }}` |

- If you attached files via WYSIWYG editor prepare for the pain of trying to locate and re-link those files later.
- Install CMS 2.0
- Import CMS Seeds with `rake comfy:cms_seeds:import[folder_name,site_identifier]`

Feel free to update this Wiki entry if you had to do this migration.
