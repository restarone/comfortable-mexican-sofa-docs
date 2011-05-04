# Sites

This functionality allows you to run multiple sites from single ComfortableMexicanSofa installation. To enable this, go to [/config/initializers/comfortable\_mexican\_sofa.rb](https://github.com/twg/comfortable-mexican-sofa/blob/master/config/initializers/comfortable_mexican_sofa.rb) and set `config.enable_multiple_sites` to true. Restart the server and now you should see **Sites** tab visible in the admin area.

Each site is attached to a particular hostname and it has a distinct set of Layouts, Pages and Snippets. You can only see those depending under what hostname you are in the admin area.