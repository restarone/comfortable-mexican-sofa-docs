Password protecting CMS pages is easy. All you need to do is create a module with `authenticate` method. Like so:

```ruby
  module CmsPagesAuth
    def authenticate
      redirect_to login_path unless current_user
    end
  end
```

Then in the initializer un-comment and change following line to this:

```ruby
config.public_auth = 'CmsPagesAuth'
```

Inside that method you have access to `@cms_site`, `@cms_layout` and `@cms_page` so you can use those in your authentication logic. Please note that this authentication only happens when requested page is found.

Here's example of how to protect `/secret/page/path` page with BasicAuth

```ruby
module CmsPagesAuth
  def authenticate
    protected_paths = ['/secret/page/path', '/so/very/protected', '/no-access']
    return unless protected_paths.member?(@cms_page.full_path)
    authenticate_or_request_with_http_basic do |username, password|
      username == 'secret_username' && password == 'secret_password'
    end
  end
end
```