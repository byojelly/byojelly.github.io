---
layout: post
title:  "Allow myself to introduce... Myself"
date:   2017-07-16 23:16:35 +0000
---



Scenario - Your coding different classes, let's say user profiles, and you find that you are repeating a lot of the same code in each class that you are writing.   Wouldn't you want to save your self time and energy to write the code once and if you need to change the code, you only have to change it in one location.  Ruby gives us a great way of doing this called modules.

Modules allow programers the ability to repeat code in new classes.

Let's try to use a module in an example. Going back to user profiles, we are going to create a default user as a module with certain behaviors that can be repeated for new users that we make. 

```
module DefaultUser
     def initialize (name)
		      @name = name
		      puts "Hello #{name}.  We are so happy you are here!"
		 end
     
		 def change_name(name)
		      @name = name
					puts "Oh cool.  You changed you name to #{name}.  I'll make sure I remember that!"
		 end
end
```

Above we wrote some simple code that allows a name to be initialize at the creation of the instance while also giving functionality to change the name of the innstance's name attribute.  If you notice, the module at this point is only utilizing instance methods.

```
class Student
     attr_accessor :name
     include DefaultUser
end
```

Our student code above uses "include" which imports the module's information so that the methods will be treated inside the Student class as instance methods. 

```
class Teacher
     attr_accessor :name :student
		 include DefaultUser
		 
		 def initialize(name, student)
		      super
					@student = student
		 end
```

The code above for a teacher calls the DefaultUser module with a twist.  We also want our teacher class to have a student so re-wrote the initialize method to include a 2nd argument teahcer.  Within the initialize method, we include super, which passes on all of the code from the module.  Under super, we add additional functionality that we want our teacher method to do (in this case use the student argument to define the student attribute). 

So far we have defined this module using instance methods to be used.  What if we want some methods in our module to act as instance methods and other methods to work as class modules.  You can do this be further nesting modules  when you set them up.  For example:

```
module DefaultUser
				module InstanceMethod
								def initialize (name)
										@name = name
										self.all << self
										puts "Hello #{name}.  We are so happy you are here!"
								end

								def change_name(name)
										@name = name
										puts "Oh cool.  You changed you name to #{name}.  I'll make sure I remember that!"
								end
				end
				module ClassMethod
								def all
									self.all
								end
				end
end
```
```
class Student
     attr_accessor :name
		 @@all = []
     include DefaultUser::InstanceMethod
		 extend  DefaultUser::ClassMethod
 
end
```
class Teacher
     attr_accessor :name :student
		 @@all = []
     include DefaultUser::InstanceMethod
		 extend  DefaultUser::ClassMethod
		 
		 def initialize(name, student)
		      super
					@student = student
					
		 end
```


In order to distinguish our nested Instance module vs Class module, we call upon it using include Default::InstanceMethod  and extend::DefaultUserMethod.

Our code now has the ability to use the module's instance and class methods within new classes.   


