Password protecting CMS pages is easy. All you need to do is create a module with `authenticate` method. Like so:

    module CmsPagesAuth
      def authenticate
        redirect_to login_path unless current_user
      end
    end

Then in the initializer un-comment and change following line to this:

   config.public_auth = 'CmsPagesAuth'

Inside that method you have access to `@cms_site`, `@cms_layout` and `@cms_page` so you can use those in your authentication logic. Please note that this authentication only happens when requested page is found.