Reuse Devise ( Authentication with gem 'devise') and CanCan (Authorization with
gem 'cancan') for access control :

in `lib/my_app/devise_auth.rb`

```ruby
module MyApp::DeviseAuth
  def authenticate
    if current_user
      ability = Ability.new(current_user)
      return true if ability.can?(:manage, "Cms::Site")
      raise CanCan::AccessDenied
    else
      scope = Devise::Mapping.find_scope!(:user)
      session["#{scope}_return_to"] = new_cms_admin_site_path(:locale => I18n.locale) # if localized...
      redirect_to admin_sign_in_path
    end
  end
end
```

In `config/initializers/comfortable_mexican_sofa.rb`

```ruby
  config.admin_auth = 'MyApp::DeviseAuth'
```

In `models/ability.rb`

```ruby
def initialize(user)
  alias_action :index, :show, :to => :read
  alias_action :create, :update, :to => :manage

  # define user abilities here ....
  user ||= User.new
  ...
  if user.has_role? :admin
    can [:read, :manage], "Cms::Site"
```
