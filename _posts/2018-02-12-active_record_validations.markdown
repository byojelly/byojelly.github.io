---
layout: post
title:      "Active Record Validations"
date:       2018-02-12 12:41:27 +0000
permalink:  active_record_validations
---


As we know, Active Record gives developers the ability to create and utlize business objects within our programs while also providing storage capabilities with databases.  When setting up our databases, we define input value types to ensure that our programs and programmers understand what kind of data we are interpreting so that we can perform calculations and queries without error.  However, how do we safeguard our databases and the information that we collect within them?

The answer is validations.  Validations allow our programs to verify the accuracy of the type of data we are using before the data is persisted into the database.  Luckily, Active Record has a framework of validation methods which we can use.  

At what point in time in our programs do validations occur?  Validations occur before the data is persisted (saved) to the database.  As long as validations are put in place, methods such as: create, create!, save, save!, update, update! trigger our validations before saving to the database.

Within the Model Views Controller (MVC) framework, our validations are placed in our models file.  For example, lets say we have a Person table in our database which has a name attribute set to string.  The following would be an example of setting a validation that requires the presence of the name attribute when saving a new Person object to the database.

```

class Person < ApplicationRecord
  validates :name, presence: true
end

```

Now there are many more different types of validations that we can use, but we will get to that later. 


Valid? Method

Continuing from our Person example, before saving to a database, we can use the method valid as a quick check against our validation in our model? This is useful as this validation can take place before persisting to the database

```

p = Person.new
            # => #<Person id: nil, name: nil>
p.errors.messages
            # => {}

p.valid?
            # => false
p.errors.messages
            # => {name:["can't be blank"]}
						
p = Person.create
           # => #<Person id: nil, name: nil>
p.errors.messages
           # => {name:["can't be blank"]}
```

In the above code snippet you can see that we created a new instance of a Person without a name. Our valid? method checks against our validations in our model file and sees that eWith this validation in place, we are unable to save to our database unless a name attribute is passed on the the instance.   In our example you can also see how validation error messages work.  By passing the method .errors or .errors.messages to our instance, we can see the error messages that would arise if the validation where to be triggered.

Now that we have gone over some of the basics of validations, lets go over some use cases of different validations that we can use!  This material is also available [here](http://http://guides.rubyonrails.org/active_record_validations.html).


Acceptance
```
class Person < ApplicationRecord
  validates :terms_of_service, acceptance: { message: 'must be abided' }
end
```
* This method validates that a checkbox on the user interface was checked when a form was submitted. This is typically used when the user needs to agree to your application's terms of service, confirm that some text is read, or any similar concept.
* As you can see, a new element message can be added to your validation which personalizes the error message. 

Confirmation
```
class Person < ApplicationRecord
  validates :email, confirmation: { case_sensitive: false }
end
```
in view template 

```
<%= text_field :person, :email %>
<%= text_field :person, :email_confirmation %>
```
* You should use this helper when you have two text fields that should receive exactly the same content. For example, you may want to confirm an email address or a password. 
* In this code you can also see the nifty case_sensitive validation which comes in handy when checking if a username or email already exists in a database (also known as uniqueness which we will talk about shortly

Format
```
class Product < ApplicationRecord
  validates :legacy_code, format: { with: /\A[a-zA-Z]+\z/,
    message: "only allows letters" }
end
```

Inclusion
```
class Coffee < ApplicationRecord
  validates :size, inclusion: { in: %w(small medium large),
    message: "%{value} is not a valid size" }
end
```
* This helper validates that the attributes' values are included in a given set. In fact, this set can be any enumerable object.
* The inclusion helper has an option :in that receives the set of values that will be accepted. The :in option has an alias called :within that you can use for the same purpose, if you'd like to.

Length
```
class Person < ApplicationRecord
  validates :name, length: { minimum: 2 }
  validates :bio, length: { maximum: 500 }
  validates :password, length: { in: 6..20 }
  validates :registration_number, length: { is: 6 }
end
```

Numercality
```
class Player < ApplicationRecord
  validates :points, numericality: true
  validates :games_played, numericality: { only_integer: true }
end
```
* Besides :only_integer, this helper also accepts the following options to add constraints to acceptable values:

:greater_than - Specifies the value must be greater than the supplied value. The default error message for this option is "must be greater than %{count}".
:greater_than_or_equal_to - Specifies the value must be greater than or equal to the supplied value. The default error message for this option is "must be greater than or equal to %{count}".
:equal_to - Specifies the value must be equal to the supplied value. The default error message for this option is "must be equal to %{count}".
:less_than - Specifies the value must be less than the supplied value. The default error message for this option is "must be less than %{count}".
:less_than_or_equal_to - Specifies the value must be less than or equal to the supplied value. The default error message for this option is "must be less than or equal to %{count}".
:other_than - Specifies the value must be other than the supplied value. The default error message for this option is "must be other than %{count}".
:odd - Specifies the value must be an odd number if set to true. The default error message for this option is "must be odd".
:even - Specifies the value must be an even number if set to true. The default error message for this option is "must be even".
By default, numericality doesn't allow nil values. You can use allow_nil: true option to permit it.


Presence
```
class Person < ApplicationRecord
  validates :name, :login, :email, presence: true
end

```

Uniqueness
```
class Account < ApplicationRecord
  validates :email, uniqueness: true
end
```



There are many more types of validations that you can use. This  [rails guide](http://http://guides.rubyonrails.org/active_record_validations.html) about validations is a great resource about validations that you can use to improve your code.




