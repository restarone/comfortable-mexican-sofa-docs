With a clean install, following the exact instructions on the 'getting started page' running Rails 4.1.1 I can get as far as logging in to create the first site, but then I get this error

``Showing /home/john/.rvm/gems/ruby-2.1.2@comfy/gems/comfortable_mexican_sofa-1.12.1/app/views/layouts/comfy/admin/cms/_head.html.haml where line #6 raised:`

`File to import not found or unreadable: jquery.ui.all.`
`Load paths:`
  `/home/john/ruby_projects/research/comfy/app/assets/images`
  `/home/john/ruby_projects/research/comfy/app/assets/javascripts`
  `/home/john/ruby_projects/research/comfy/app/assets/stylesheets`
  `/home/john/ruby_projects/research/comfy/vendor/assets/javascripts`
  `/home/john/ruby_projects/research/comfy/vendor/assets/stylesheets`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/comfortable_mexican_sofa-1.12.1/app/assets/images`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/comfortable_mexican_sofa-1.12.1/app/assets/javascripts`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/comfortable_mexican_sofa-1.12.1/app/assets/stylesheets`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/bootstrap-sass-3.1.1.1/vendor/assets/fonts`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/bootstrap-sass-3.1.1.1/vendor/assets/javascripts`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/bootstrap-sass-3.1.1.1/vendor/assets/stylesheets`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/tinymce-rails-4.1.0/app/assets/javascripts`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/tinymce-rails-4.1.0/app/assets/source`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/tinymce-rails-4.1.0/vendor/assets/javascripts`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/codemirror-rails-4.2/vendor/assets/javascripts`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/codemirror-rails-4.2/vendor/assets/stylesheets`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/jquery-ui-rails-5.0.0/app/assets/images`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/jquery-ui-rails-5.0.0/app/assets/javascripts`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/jquery-ui-rails-5.0.0/app/assets/stylesheets`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/bootstrap_form-2.1.1/app/assets/stylesheets`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/turbolinks-2.2.2/lib/assets/javascripts`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/jquery-rails-3.1.1/vendor/assets/javascripts`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/coffee-rails-4.0.1/lib/assets/javascripts`
  `/home/john/.rvm/gems/ruby-2.1.2@comfy/gems/bootstrap-sass-3.1.1.1/vendor/assets/stylesheets`
  `(in /home/john/.rvm/gems/ruby-2.1.2@comfy/gems/comfortable_mexican_sofa-1.12.1/app/assets/stylesheets/comfortable_mexican_sofa/application.css.sass:1)``

It's similar to issue #308 but notice that the file name it's reporting missing is different.
