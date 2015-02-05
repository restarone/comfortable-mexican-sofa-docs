When working with image files you may need to change the size to allow them to work with different different parts of your website. Comfy CMS makes this easy by allowing users to add image sizes in their config file. 

Inside of config/comfortable_mexican_sofa.rb 

    ComfortableMexicanSofa.configure do |config|
      config.upload_file_options[:styles] = { menu_item: '175x115>', thumb: '100x100<', medium: '300x300<'}
    end

upload_files_options[:styles] accepts a hash with the name of the file size you want to use throughout the site and a string with the file_size. 