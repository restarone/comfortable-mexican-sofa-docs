Do you have other authentication system in place (like Devise, AuthLogic, etc)
and wish to use that? For that, you will need to create a module that does the
authentication check and make ComfortableMexicanSofa use it. For example:

```ruby
module CmsDeviseAuth
  def authenticate
    unless current_user && current_user.admin?
      redirect_to new_user_session_path
    end
  end
end
```

You can put this module in /config/initializers/comfortable\_mexican\_sofa.rb and change authentication method:

```ruby
config.admin_auth = 'CmsDeviseAuth'
```

Now to access Sofa's admin area users will be authenticated against your existing authentication system.
