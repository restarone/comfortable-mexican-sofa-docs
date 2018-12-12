Because of:

- Migrating from Paperclip to ActiveStorage
- Change of CMS tag structure, including format of tags as well as commands
- Removal of Mirrored sites functionality and adding page translations

It's not that easy to upgrade 1.12 install to the current 2.0 version. The reinstallation path is probably safer, but if you want to live dangerously, see below for an upgrade-in-place path.

# Safe (Reinstallation) Option
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
  content_tag = path.include?('/pages/') ? '[textarea content]' : '[content]'
  File.delete(attributes_path)
  if path.include? '/snippets/'
    File.delete(path)
    Dir.rmdir(File.dirname(path))
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

- Remove all `block:` lines in the YAML in `files/`
- If you attached files via WYSIWYG editor prepare for the pain of trying to locate and re-link those files later (you may be able to use filenames and some of the ActiveStorage migration documents below to do so)
- Install CMS 2.0
- Import CMS Seeds with `rake comfy:cms_seeds:import[folder_name,site_identifier]`
- If you previously used cms_manageable, it will need to be reimplemented as the WithFragments concern. See this [wiki page](https://github.com/comfy/comfortable-mexican-sofa/wiki/Render-Non-Comfy-Models-as-Pages) for guidance.

# Upgrade-in-Place Option

It is possible to upgrade in place. The difficulty level of the upgrade will vary tremendously on your usage patterns and how much custom code you have in place. Our installation had enough attached files from the WYSIWYG editor that it was worth the additional effort on that point alone.

Key differences from 1.12 to 2.0:
* upgrade to Rails 5.2 from whichever version you were using. This upgrade may require upgrading other gems, updating to current best practices, etc., but will be necessary to run CMS 2.0
* `Comfy::Cms::Blocks` have become `Comfy::Cms::Fragments`, belong to a `record` instead of a `blockable`, and there are a few other schema changes that can get a bit tricky if your code is particularly integrated
* migration from Paperclip to ActiveStorage. 
* updating layout tags to the new style

## Schema changes, especially Fragments and Translations
The two biggest changes to the database schema for CMS 2.0 are the new Translations table and renaming `Blocks` to `Fragments`. `Fragments` belong to a `record` rather than a `blockable`, and the fragments table also has three additional columns. See the migration below.

Obviously, any code or query referring to any of the renamed classes or attributes will need to be updated. **This includes helper methods**; calls to `cms_block_content` will need to be calls to `cms_fragment_content`, for example.

Also, `comfy_cms_files.label` now has a default value of an empty string. Failing to change this will break file uploading.

```ruby
class RenameComfyCmsBlocksToComfyCmsFragments < ActiveRecord::Migration[5.2]
  def change
    rename_table :comfy_cms_blocks, :comfy_cms_fragments
    rename_column :comfy_cms_fragments, :blockable_id, :record_id
    rename_column :comfy_cms_fragments, :blockable_type, :record_type
    add_column :comfy_cms_fragments, :tag, :string, null: false, default: 'text'
    add_column :comfy_cms_fragments, :datetime, :datetime
    add_column :comfy_cms_fragments, :boolean, :boolean, null: false, default: false
    change_column :comfy_cms_files, :label, :string, null: false, default: ''
    change_column :comfy_cms_files, :file_file_name, :string, null: true
    remove_column :comfy_cms_files, :file_content_type
    remove_column :comfy_cms_files, :file_file_size
    remove_index :comfy_cms_sites, :is_mirrored
    remove_column :comfy_cms_sites, :is_mirrored
    remove_column :comfy_cms_layouts, :is_shared
    remove_column :comfy_cms_pages, :is_shared
    remove_column :comfy_cms_snippets, :is_shared

    limit = 16777215
    create_table :comfy_cms_translations, force: true do |t|
      t.string  :locale,    null: false
      t.integer :page_id,   null: false
      t.integer :layout_id
      t.string  :label,           null: false
      t.text    :content_cache,   limit: limit
      t.boolean :is_published,    null: false, default: true
      t.timestamps

      t.index [:page_id]
      t.index [:locale]
      t.index [:is_published]
    end

  Rake::Task['cms_update_2:update_cms_tags'].invoke
  end
end
```
The Rake task invoked is discussed below (under Updating Tags). There is at least one other column (`comfy_cms_files.block_id`) that is no longer used by Comfy but that may be useful during migration.

Note that the migration above leaves the `comfy_cms_files.file_file_name` column in place but allows nulls; this allows for using that value during migration to Active Storage. Removing the column after migration is probably a good idea.

## Other code changes
While I'm sure there are more code changes than I've noted, these required changes to our code:
* we had a customer controller inheriting from `Comfy::Cms::ContentController` that was not explicitly setting `@cms_page` and `@cms_layout`, which now need to be set before calling `render_page`
* As noted above, `load_fixtures` has been superseded by `load_seeds`

## Migrating from Paperclip to ActiveStorage
While largely beyond the scope of this document, reattaching all of your Comfy::Cms::File attachments by hand does not sound like fun. For background and possible migration paths, see also 
* https://gorails.com/episodes/migrate-from-paperclip-to-rails-active-storage
* https://www.reddit.com/r/rails/comments/8gif2j/paperclip_is_dead_time_to_start_using/
* https://kyleke.es/posts/2018/04/migrating-from-paperclip-to-activestorage
* https://github.com/thoughtbot/paperclip/blob/master/MIGRATING.md

In short, you'll need to first configure ActiveStorage and then somehow convince CMS to attach the original (and now disconnected) asset to the appropriate ActiveStorage object. If you're currently using rmagick for transformations, you may want to make the effort to install minimagick for transformations; the syntax is often different depending on which image processor you use.

The guides above may give some ideas; if you're using standard filesystem storage, it can be done even more easily:

```ruby    
task :reattach_files => :environment do |t|
  files_directory = Rails.root.join("public/system/files")
  Dir.children(files_directory).each do |f|
    Dir.children(files_directory.join("#{f}/original")).each do |file| 
      comfy_file = Comfy::Cms::File.find(Integer(f))
      local_path = files_directory.join("#{f}/original/#{file}")
      puts "Attaching #{local_path} to File #{f}"
      comfy_file.attachment.attach io: File.open(local_path), filename: comfy_file.file_file_name
    rescue ActiveRecord::RecordNotFound
      warn "Did not find Comfy::Cms::File #{f}"
    end
  end
end
```
Note that this rake task could easily be tweaked to pull files from S3 or another cloud provider, as long as you can determine the appropriate URL to download.

If you have any Paperclip styles defined, you'll need to update any references to those images to use variants instead. See the above migration docs for details.

Also, note that this migration relies on the Paperclip file_file_name field. Once you have completed the migration, you'll probably want to remove the Paperclip columns. If you don't remove them, you will need to at least allow null values or file uploads will fail.

### Page attachments
Page attachments are handled sufficiently differently to cause a bit of work. In my case, I found it easier to migrate each page attachment to a text reference to the Comfy::Cms::File object id and then adjust from there, but it should be possible to instead reattach the blob to the fragment itself.

How I did it, using the vestigial `block_id` value in the `comfy_cms_files` table:
```ruby
task :reattach_page_files => :environment do |t|
  files = Comfy::Cms::File.where.not(block_id: nil)
  files.each do |f|
    unless f.attachment.attachment.nil?
      fragment = Comfy::Cms::Fragment.find(f.block_id)
      puts "Attaching File #{f.id} to fragment #{fragment.id}"
      fragment.content = f.id
      fragment.tag = "text"
      fragment.attachments.purge
      fragment.save
    else
      puts "Error: Attachment for File #{f.id} is nil, did not attach to fragment #{f.block_id}"
    end
  rescue ActiveRecord::RecordNotFound
    warn "Did not find Comfy::Cms::Fragment #{f.block_id}"
  end
end
```
The below **may** actually reattach the blobs, but I haven't tested it:
```ruby
task :reattach_page_files => :environment do |t|
  files = Comfy::Cms::File.where.not(block_id: nil)
  files.each do |f|
    unless f.attachment.attachment.nil?
      fragment = Comfy::Cms::Fragment.find(f.block_id)
      puts "Attaching File #{f.id} to fragment #{fragment.id}"
      fragment.attachments.attach f.attachment.attachment.blob # note that the blob is to be attached, not the attachment
      fragment.tag = "file"
      fragment.save
    else
      puts "Error: Attachment for File #{f.id} is nil, did not attach to fragment #{f.block_id}"
    end
  rescue ActiveRecord::RecordNotFound
    warn "Did not find Comfy::Cms::Fragment #{f.block_id}"
  end
end
```
## Updating tags
The content/layout tagging syntax has changed. Please see the appropriate Wiki entries and source code for more details, but you will need to change any existing tags in your layouts and such. The regular expressions listed above proved a good starting point for my upgrade, but I ended up with a lot more. The rake task I used clearly could be cleaned up substantially; I was testing iteratively and adding / updating new lines each time I came across a tag that didn't get converted cleanly. Further clean-up would be necessary to make it work across all installations.

## cms_manageable
- If you previously used cms_manageable, it will need to be reimplemented as the WithFragments concern. See this [wiki page](https://github.com/comfy/comfortable-mexican-sofa/wiki/Render-Non-Comfy-Models-as-Pages) for guidance.

A few notes:
* rich_text fields are now wysiwyg fields
* unless you reattach files, the tags referring to them will be broken
* if you do reattach them, you'll presumably need to update the syntax
* apologies for making your eyes bleed with the mess below, **please** update the wiki entry if you do the upgrade and clean up and consolidate the regular expressions properly

```ruby
task :update_cms_tags => :environment do |t|
  Comfy::Cms::Layout.all.each do |layout|
    layout.content = layout.content.gsub(/\{\{ ?cms:page:([\w\/]+) ?\}\}/, '{{ cms:text \1 }}') if layout.content.is_a? String
    
    # {{cms:page:page_header:string}} -> {{ cms:text page_header }}
    layout.content = layout.content.gsub(/\{\{ ?cms:page:([\w]+):string ?\}\}/, '{{ cms:text \1 }}') if layout.content.is_a? String
    
    # {{cms:page:content:rich_text}} -> {{ cms:wysiwyg content }}
    layout.content = layout.content.gsub(/\{\{ ?cms:page:([\w]+):rich_text ?\}\}/, '{{ cms:wysiwyg \1 }}') if layout.content.is_a? String
    layout.content = layout.content.gsub(/\{\{ ?cms:page:([\w]+):([^:]*) ?\}\}/, '{{ cms:\2 \1 }}') if layout.content.is_a? String
    layout.content = layout.content.gsub(/\{\{ ?cms:field:([\w]+):string ?\}\}/, '{{ cms:text \1, render: false }}') if layout.content.is_a? String
    layout.content = layout.content.gsub(/\{\{ ?cms:field:([\w]+):([^:]*) ?\}\}/, '{{ cms:\2 \1, render: false }}') if layout.content.is_a? String

    # {{ cms:partial:main/homepage }} -> {{ cms:partial "main/homepage" }}
        layout.content = layout.content.gsub(/\{\{ ?cms:asset:([\w\/-]+):([\w\/-]+):([\w\/-]+) ?\}\}/, '{{ cms:asset \1 type: \2 as: tag}}') if layout.content.is_a? String
        layout.content = layout.content.gsub(/\{\{ ?cms:partial:([\w\/]+) ?\}\}/, '{{ cms:partial \1 }}') if layout.content.is_a? String
        layout.content = layout.content.gsub(/\{\{ ?cms:(\w+):([\w\/-]+) ?\}\}/, '{{ cms:\1 \2 }}') if layout.content.is_a? String
        layout.content = layout.content.gsub(/\{\{ ?cms:(\w+):([\w\/-]+):([\w\/-]+):([\w\/-]+) ?\}\}/, '{{ cms:\1 \2 \3 \4}}') if layout.content.is_a? String
        layout.content = layout.content.gsub(/\{\{ ?cms:(\w+):([\w]+):([^:]*) ?\}\}/, '{{ cms:\1 \2, "\3" }}') if layout.content.is_a? String
        layout.content = layout.content.gsub(/cms:rich_text/, 'cms:wysiwyg') if layout.content.is_a? String
        layout.content = layout.content.gsub(/cms:integer/, 'cms:number') if layout.content.is_a? String
        layout.content = layout.content.gsub(/cms: string/, 'cms:text') if layout.content.is_a? String # probably a result of goofing one of the more general regexps
        layout.content = layout.content.gsub(/\{\{ ?cms:page_file ([\w\/]+) ?\}\}/, '{{ cms:file \1, render: false }}') if layout.content.is_a? String
        layout.content = layout.content.gsub(/<!-- {{ cms:text (\w+)_slide, render: false }} -->/, "{{ cms:text \1, render: false }}") if layout.content.is_a? String

    layout.save if layout.changed?
  end
  Comfy::Cms::Fragment.all.each do |fragment|
    # {{ cms:partial:main/homepage }} -> {{ cms:partial "main/homepage" }}
    fragment.datetime = fragment.updated_at if fragment.datetime.nil?
    fragment.content = fragment.content.gsub(/\{\{ ?cms:partial:([\w\/]+) ?\}\}/, '{{ cms:partial \1 }}') if fragment.content.is_a? String

    fragment.content = fragment.content.gsub(/\{\{ ?cms:page:([\w]+):string ?\}\}/, '{{ cms:text \1 }}') if fragment.content.is_a? String
    fragment.content = fragment.content.gsub(/\{\{ ?cms:page:([\w]+):rich_text ?\}\}/, '{{ cms:wysiwyg \1 }}') if fragment.content.is_a? String

    fragment.content = fragment.content.gsub(/\{\{ ?cms:page:([\w\/]+) ?\}\}/, '{{ cms:text \1 }}') if fragment.content.is_a? String
    fragment.content = fragment.content.gsub(/\{\{ ?cms:page:([\w]+):([^:]*) ?\}\}/, '{{ cms:\2 \1 }}') if fragment.content.is_a? String
    fragment.content = fragment.content.gsub(/\{\{ ?cms:field:([\w]+):([^:]*) ?\}\}/, '{{ cms:\2 \1, render: false }}') if fragment.content.is_a? String

    fragment.content = fragment.content.gsub(/\{\{ ?cms:(\w+):([\w]+) ?\}\}/, '{{ cms:\1 \2 }}') if fragment.content.is_a? String
    fragment.content = fragment.content.gsub(/\{\{ ?cms:(\w+):([\w]+):([^:]*) ?\}\}/, '{{ cms:\1 \2, "\3" }}') if fragment.content.is_a? String
    fragment.save if fragment.changed?
  end

  # With the change from Block to Fragment, Revision.data hash keys need to be updated
  Comfy::Cms::Revision.all.each do |revision|
    if revision.data['blocks_attributes'].present?
      revision.data['fragments_attributes'] = revision.data['blocks_attributes']
      revision.data.delete('blocks_attributes')
      revision.save
    end
  end
end
```

Feel free to update this Wiki entry if you had to do this migration.
