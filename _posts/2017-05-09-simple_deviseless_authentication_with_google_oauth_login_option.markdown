---
layout: post
title:  "Simple Deviseless Authentication with Google OAuth Login Option"
date:   2017-05-09 17:40:35 -0400
---


I recently developed a Rails-based [law firm billing application](https://github.com/bentonwong/law-firm-billing-software).  The application allows lawyers (the users) at a law firm to track their time for client matters, so that the firm can bill the clients for services rendered.

The authentication employed here allows users to sign up and sign in using either a typical email/password process or through an [OAuth](https://www.sitepoint.com/rails-authentication-oauth-2-0-omniauth/) from a third party service.  This application developed here uses Google as its third party OAuth service.

I found several, easy to follow guides on implementing Google Oauth into a Rails in my initial research; here are two, well written ones:

1. https://richonrails.com/articles/google-authentication-in-ruby-on-rails/
2. http://www.jessespevack.com/blog/2016/10/16/how-to-test-drive-omniauth-google-oauth2-for-your-rails-app

However, such guides do not go into detail on integrating OAuth alongside a typical login/signup authentication system.

# The Process

I developed this general process below to handle login/sign ups through either channels:

1. Determine if a provider (in this case, Google) is given in the params (e.g. !params[:provider].nil?) passed in by the new session request.  I noticed that OAuth generates params with provider, while the normal login/signup does not.  Therefore, the process checks for this first:

``` 
def create
    if !params[:provider].nil?
      validate_oauth
    elsif params[:lawyer][:email].blank? || params[:lawyer][:password].blank?
      redirect_to_signin_form_with_errors('ALERT: Email or password cannot be left blank!')
    else
      validate_signin
    end
end
```

2. If params[:provider] is not nil, I would then pass the params hash onto a method to see if the lawyer already exists in the database; a new lawyer would be created if none existed or update that existing lawyer with information passed in through Google.  And then, a new session would be started if successful.

```
def validate_oauth
   @lawyer = Lawyer.update_or_create(env["omniauth.auth"])
    if @lawyer
       start_new_session
    else
       redirect_to_signin_form_with_errors('Alert: Invalid credentials!')
     end
end
```

```
def self.update_or_create(auth)
    lawyer = Lawyer.find_by(email: auth[:info][:email]) || Lawyer.new
    lawyer.attributes = {
      provider: auth[:provider],
      uid: auth[:uid],
      email: auth[:info][:email],
      name: auth[:info][:name],
      oauth_token: auth[:credentials][:token],
      oauth_expires_at: auth[:credentials][:expires_at]
    }
    lawyer.save!
    lawyer
  end
	```

3. To accommodate the situation where the lawyer has already set a password from a previous session or the lawyer never sets a password because they have always logged in via OAuth, I used this snippet to generate a random password if no password for the lawyer existed:

`lawyer.password = SecureRandom.hex(9) if !lawyer.password_digest`

4. On the other hand, if params[:provider] is found to be nil, then the authentication process would be directed to the standard log in/sign up process below.

```
def validate_signin
   @lawyer = Lawyer.find_by(email: params[:lawyer][:email])
   if !!@lawyer && @lawyer.authenticate(params[:lawyer][:password])
      start_new_session
   else
      redirect_to_signin_form_with_errors('ALERT: Email and/or password are incorrect!')
   end
end

def start_new_session
   session.clear
   session[:lawyer_id] = @lawyer.id
   redirect_to @lawyer
end
```

# Final Thoughts

Because of the abstract nature of Devise, I built my own authentication system with a `has_secure_password` requirement in the user model and `password_digest` column in the users table. It made studying and debugging the application easier.

Integrating Google OAuth was already complex in itself.  However, using my own autentication system made it much easier to put the two together.

Devise is an excellent authentication solution if properly implemented as I discussed in my [previous blog entry](http://keeponmovingforward.com/2017/05/05/devise_in_a_nutshell/).  However, for prototyping purposes, this worked just as well.
