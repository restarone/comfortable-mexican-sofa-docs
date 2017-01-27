Here is what you need to do for deploying your comfy app to heroku:

1. Read the heroku guide on deploying a Rails 5 app to [https://devcenter.heroku.com/articles/getting-started-with-rails5](https://devcenter.heroku.com/articles/getting-started-with-rails5).
This also covers many basics like putting your app on git, using .env and installing the heroku toolbelt.
Ideally, you do all this before adding comfy to your app. At least the switch to the postgresql database. Otherwise you will need to repeat the db setup and content filling.

2. Make sure you switch paperclip's storage to Amazon S3. Heroku does not allow file system storage. Add the gem ‘aws-sdk’ to your Gemfile, add the necessary ENV keys to your .env file and add the configuration for paperclip to your application.rb. The entry could look like this:

>     # configuring paperclip for Amazon AWS S3 storage:
>     config.paperclip_defaults = {
>       :storage => :s3,
>       :bucket => ENV['S3_BUCKET_NAME'],
>       :s3_host_name => "s3-eu-central-1.amazonaws.com",
>       :s3_region => "eu-central-1",
>       :s3_credentials => {
>         :access_key_id => ENV['AWS_ACCESS_KEY_ID'],
>         :secret_access_key => ENV['AWS_SECRET_ACCESS_KEY'],
>       },
>       :s3_protocol => '',
>       :url => "/:class/:attachment/:id_partition/:style/:filename",
>       :path => "/:class/:attachment/:id_partition/:style/:filename"
>     }