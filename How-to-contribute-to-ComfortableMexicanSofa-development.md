GitHub makes it all too easy:

* Fork the project
* Start a feature/bugfix branch (don't just work on the master branch)
* Commit and push until you are happy with your contribution
* Create a Pull Request

ComfortableMexicanSofa is an engine so you can run it as a standalone for development purposes (you can run it in production too, but hey). Clone your fork into a directory, run `bundle install` and then `rake db:migrate`. Feel free to change Gemfile if you want to work against a particular Rails version. Just don't commit it later.

You run tests as normal: `rake tests`

As far as conventions go, there's only one rule: Erb/Css/UnitTest only please.