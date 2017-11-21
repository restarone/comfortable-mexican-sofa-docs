Here is what you need to do for deploying your comfy app to heroku:

1. Read the heroku guide on deploying a Rails 5 app to [https://devcenter.heroku.com/articles/getting-started-with-rails5](https://devcenter.heroku.com/articles/getting-started-with-rails5).
This also covers many basics like putting your app on git, using .env and installing the heroku toolbelt.
Ideally, you do all this before adding comfy to your app. At least the switch to the postgresql database. Otherwise you will need to repeat the db setup and content filling.

2. Make sure you switch ActiveStorage storage to Amazon S3. Heroku does not allow file system storage.
