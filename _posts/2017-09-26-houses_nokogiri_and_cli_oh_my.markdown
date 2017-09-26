---
layout: post
title:  "Houses, nokogiri, and cli oh my!"
date:   2017-09-26 11:08:03 +0000
---


I am extremely happy to be publishing this issue of my blog after the completion of CLI scraping project.  This project took a long time to complete mainly because of tawo reasons:

1.  My wife and I have just purchased and successfully closed on our first home!
2.  The folder setup structure was difficult at first to understand.

My wife and I have been looking at homes for sometime now (almost 2 years) and we have come very close to buying several homes with them falling through half way through the process for unforseen circumstances in the home inspection.  To say that obtaining a mortgage and buying a home is a complicated process does not give it the credit it deserves. Although it was quite the hair pulling process, at this time in our lives we could not be happier and more excited for what the future will bring.

Given the diffficult nature of buying our first home, I found it rather difficult to manage my self study with coding along with my full time job.  However now that things have slowed down I look forward to getting back into the swing of things and resuming my previous pace with Flatiron's program.

This project has the developer design the entire cli platform from the ground up.  Up until this point I have felt confident in my coding abilities. However a major mental blocked developed for me during the initial setup of the folder structure for the project.  I started off trying to replicate the fodler structure of example projects that were listed in conjunction with the directions for the project.  But this approach led me to become more confused.

After reading through the project's setup materials I then came across an extremely helpful link for a tutrorial project that provided the context I needed to setup the shell of my project. After breaking down the video over and over to extract the instructions that I needed I learned some very useful tools towards setting up the folder/environment structure.

An overview of those tools include:

To begin with:
* In your terminal type: "bundle gem name_of_project"
* this will create the folder structure you want

You want to start your programming with a shell of what the cli should do then you can refine the scraping and advanced methods after you have your program working on  the surface.

The Bin exeucatble file needs the below line of code at the top of the file so that the program knows to read the code as ruby
        #!/usr/bin/env ruby

The bin folder should contain an executable file that the user interracts with.
You can lookup the file permissions of the files in the folder by typing the following prompts into terminal as long as the terminal is set to that folder:
        "ls -lah"
        #more permissions  https://support.rackspace.com/how-to/checking-linux-file-permissions-with-ls/

when you review the permissions :
        r = read
        w = write
        x - execuctable

if your executable file does not contain x, then it is more difficult for the user to directly call the program from the cli prompt
to give executabel permission to the file you must type the following in terminal:
        "chmod +x name-of-project"
        #above name-of-project is the name of the executable file
        #after the change you can now execute the file by typing the below text directly into terminal:
            ./bin/name-of-project
        #this teaches our operating system how to interpeate ruby (using the shabing header line)

setup the bones - methods call, list, menu, goodbye
--------------------------------
then setup the higher thinking of your code
-----------
When running in terminal  ./bin/console for first time after setting up the deal.rb (under lib folder and daily_deal folder) i received the following error
              Bundler could not find compatible versions for gem "bundler":
                In Gemfile:
                  bundler (~> 1.15)

                Current Bundler version:
                  bundler (1.11.2)
              This Gemfile requires a different version of Bundler.
              Perhaps you need to update Bundler by running `gem install bundler`?

              Could not find gem 'bundler (~> 1.15)' in any of the sources

To fix this i had to open the daily_deal.gemspec file and change
                spec.add_development_dependency "bundler", "~> 1.15"
                to
                spec.add_development_dependency "bundler", "~> 1.11.2"

After this change the terminal accepted ./bin/console

----------------------
At the scraping coding point we had to add additional dependencies in daily_deal.gemspec.
Also, we have to require 'nokogiri' and require 'pry' in the lib folder project_file_name.rb file to have the dependencies come through.


Although these are a few scattered notes I took while fixing errors during my code, overcomming the obstacles became extremely gratifying at the completion of the project.

Until next time.

-Alex
