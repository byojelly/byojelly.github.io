---
layout: post
title:      "OmniAuth Oh My!"
date:       2018-04-16 23:47:49 +0000
permalink:  omniauth_oh_my
---


Oh happy day!  Today I finished preparing my rails portfolio project for review.  As I wrap up my code, I can't help but think about all of the challenging obstacles that this project presented to me. Whether configuring nested forms, forms within nested resources, or tackling the devise gem, there was always plenty of occasions to learn.  The most challenging obstacle however, was incorporating OmniAuth alongside the Devise gem.  


What is Omniauth?
“OmniAuth is a library that standardizes multi-provider authentication for web applications. It was created to be powerful, flexible, and do as little as possible.” (https://github.com/omniauth/omniauth)  This gem was created to enable rails applications to authenticate users using 3rd party website login credentials such as Facebook and Google.  The reasoning for using OmniAuth is pretty straightforward for startup companies with limited resources.  Omniauth allows developers to use the same password encryption and security protocols that major companies maintain for their applications rather than having those resources managed in house.  When a user on your platform logs in with OmniAuth, the process is simple:
1) The user selects a link such as  "Log in with Github"
2) Your application redirects the user to the Github user verification page where the user inputs their Github username and password.
3) If the username and password is correct, the provider will send information back to your app regarding the user. Your app can use this info to create a user/profile.

What is Devise?
Devise is a gem that provides applications with authentication capabilities.  Although very powerful with its abilities, it can also be complex and at times difficult to customize.

When developing my application it was challenging to find a clear example of how to implement OmniaAuth in an application that also uses Devise.   Through lots of research and coding errors, I was able to find this post (https://www.codementor.io/anaumov/rails-omniauth-with-devise--github-example-du107rmn7) which I believed gave the best tutorial on how to setup omniauth using github as the provider.  In addition, this link (https://richonrails.com/articles/google-authentication-in-ruby-on-rails/) provides great supporting information on OmniAuth without Devise.

With my experience in setting up OmniAuth functionalities for my rails project, I thought I would give a small high level tutorial on how I setup my OmniAuth authentication alongside devise. This tutorial briefly steps through my process of setting up a GitHub OmniAuth functionality which I put together after reviewing the documentation in the 2 urls that I gave to you in the previous paragrapm. 

Before starting, make sure that you have a working app built on ruby on rails that successfully uses Devise for authentication (more information on devise https://github.com/plataformatec/devise if necessary). 
1)  Setup your gems in your gemfile.
gem 'dotenv-rails'  #allows us to setup a file to store our client and secret keys for OmniAuth without submitting to github.
gem 'omniauth'  #gem to allow OmniAuth (may already exist in devise)
gem 'omniauth-github'  #activates the github for omniauth gem
2) Create a callbacks controller and add methods for each OmniAuth.
class CallbacksController < Devise::OmniauthCallbacksController
  	def github
   	 	@user = User.from_omniauth(request.env["omniauth.auth"])
   	 	@user.contact = Contact.create
   	 	sign_in_and_redirect @user
 	 end
 end
3) In config/routes.rb, add the an OmniAuth callbacks route to the controller
devise_for :users, :controllers => { :omniauth_callbacks => "callbacks"}
4) Add a migrations file with table columns uid, provider, and any other table fields necessary.
The readme of the OmniAuth provider gem will give you details about what attributes are necessary for the user table.
5) In your devise User module, activate omniauthable in devise, and setup a class method “self.from_omniauth(auth)” which will that sets the user attributes from the information received from the provider site.
Class User <ApplicationRecord
devise :omniauthable
    def self.from_omniauth(auth)
        where(provider: auth.provider, uid: auth.uid).first_or_create do |user|
          user.provider = auth.provider
          user.uid = auth.uid
          user.email = auth.info.email
          user.password = Devise.friendly_token[0,20]
        end
    end
end
6)  Create a signin application with the provider site and obtain the app key and secret code. More information on this is in the link below.
https://developer.github.com/v3/guides/basics-of-authentication/
7) My project uses the dot-env gem to hide the your apps code and secret key from posting the github.  Under your root directory, you would create a “.env” file has the the code and key.  You would then update your config/initializers/devise.rb file with the code below.
.env
GITHUB_KEY=fasdljaldskjlads
GITHUB_SECRET=ldakjalskdjdakldjalkjkdsl
config/initializers/devise.rb 
config.omniauth :github, ENV['GITHUB_KEY'], ENV['GITHUB_SECRET'], :scope => 'user:email'

And thats it!

I hope you enjoy the complex world of OmniAuth as much as I did.  Also, if you see anything in my blog that should be updated please let me know.  I am not an expert in Rails but I am just trying to learn and help share what I have learned along the way.  If you see that anything looks incorrect contact me on slack and I will update it(#byojelly)!

Until next time.

Alex
