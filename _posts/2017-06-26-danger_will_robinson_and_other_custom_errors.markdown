---
layout: post
title:  "Danger Will Robinson (and other custom errors)"
date:   2017-06-26 02:11:33 +0000
---




Currently in the program I am learning about customizing error messages (aka the exception classes).   So far, whenever I see errors appear after running code my goal has been to get rid of them by implementing the correct code to have my tests pass. But the last few lessons have flipped that methodology on its head by focusing on creating and manipulating errors to work as desired.

When developing custom errors it is important to have a basic understanding of the ruby Exception class hierarchy.  This hierarchy is:
Exception
  NoMemoryError
  ScriptError
    LoadError
    NotImplementedError
    SyntaxError
  SecurityError
  SignalException
    Interrupt
  StandardError -- default for rescue
    ArgumentError
      UncaughtThrowError
    EncodingError
    FiberError
    IOError
      EOFError
    IndexError
      KeyError
      StopIteration
    LocalJumpError
    NameError
      NoMethodError
    RangeError
      FloatDomainError
    RegexpError
    RuntimeError -- default for raise
    SystemCallError
      Errno::*
    ThreadError
    TypeError
    ZeroDivisionError
  SystemExit
  SystemStackError
	
	
The reason for this hierarchy is so that you can easily extract the exception that most relates to the error message you are trying to create.  StandardError is used most frequently for custom errors.  
	
To create a custom error, you start out by building a class that inherits the StandardError exception.

*class ExampleError < StandardError
 end*
 
 You then incorporate the error within the code you are working by using the "raise" command. For example:
 

```
class Person
  attr_accessor :partner, :name
 
  def initialize(name)
    @name = name
  end
 
  def get_married(person)
    self.partner = person
    if person.class != Person 
     raise PartnerError
    else
      person.partner = self
    end
  end
 
  class PartnerError < StandardError
  end
end
```

In the example above, we want Example Error to return when the if function is true.  At this point, when the code executes and the error is invoked, the program will stop.  Now there are some instances where we want our cod to continue processing. For those instances "rescuing" is in order. The pattern for rescuing is as follows:

*begin 
  raise YourCustomError
rescue YourCustomError
end
*

Lets implement this into a code example:


```
class Person
  attr_accessor :partner, :name
 
  def initialize(name)
    @name = name
  end
 
  def get_married(person)
    self.partner = person
    if person.class != Person
      begin
        raise PartnerError
      rescue PartnerError => error
          puts error.message
      end
    else
      person.partner = self
    end
  end
 
  class PartnerError < StandardError
    def message 
      "you must give the get_married method an argument of an instance of the person class!"
    end
  end
end
```

The example above does the following:
1. When the if condition in the get_married instance method is true, we begin, then raise the error, the rescue the error, puts the error.message.
2. We have also added a message method in our PartnerError (customized error)



You could also do this another way, like so:

*raise MyError, "My message"*

And you can add a default message to your custom error class by adding your own constructor.

```
class MyError < StandardError
  def initialize(msg="My default message")
    super
  end
end
```
 
There is one last thing to be aware of with custom errors. Notice how we inherited from StandardError in the example? That's intentional. While there is an Exception class in Ruby, you should NEVER inherit directly from it. For more information about this, check out this article about the differences between[ Exception and StandardError](http://blog.honeybadger.io/ruby-exception-vs-standarderror-whats-the-difference/)


Recap

Although it would be ideal having a personal intergallactic robot to help us with our coding and provide us with personal error messages to avoid danger and catastrophy, ruby does a nice job with inheriting the Exception class. 

