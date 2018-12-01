Sometimes you want to render you're regular app objects like a Comfy::Cms::Page. Enter the Comfy::Cms::WithFragments concern. (Note: This used to be called cms_manageable, but with the release of comfy 2.0, has been converted into a concern.)

An example from the previous implementation of this feature as cms_manageable:
````
class BoringModel < ActiveRecord::Base

  validates :is_awesome, presence: true

  cms_manageable

  # Your job to figure out a nice way to handle this...
  def layout
    Cms::Layout.new(content: "<p>{{ cms:page:random_content }}</p>")
  end

end


# Let's assume we have an instance of our BoringModel
boring_model = BoringModel.first
# Set some blocks that match the layout we defined in the class...
boring_model.blocks_attributes = [{ :identifier => 'random_content', :content => 'not so boring anymore ;-)' }]

boring_model.render
#=> "<p>not so boring anymore ;-)</p>"
````

For version 2.0+, here are the steps to take:
1. Add `include Comfy::Cms::WithFragments` in your model.
2. Add a `content_cache` column to your objects table.
3. Associate your object with a comfy layout. `Comfy::Cms::WithFragments` adds
````
belongs_to :layout, class_name: "Comfy::Cms::Layout"
````
4. Associate your object to comfy fragments which store the content that will be rendered. `Comfy::Cms::WithFragments` adds
````
has_many :fragments,
    class_name: "Comfy::Cms::Fragment",
    as:         :record,
    autosave:   true,
    dependent: :destroy
````
5. Profit!

For further information, see the `Comfy::Cms::WithFragment` module, which is also used by `Comfy::Cms::Page` to handle the relationship between comfy pages and fragments. Dogfooding for the win! Remember, blocks have been removed in comfy 2.0, and are now called fragments.

Links
* The Comfy::Cms::WithFragment concern - https://github.com/comfy/comfortable-mexican-sofa/blob/master/app/models/concerns/comfy/cms/with_fragments.rb
* The cms_manageable pull request - https://github.com/comfy/comfortable-mexican-sofa/pull/409
