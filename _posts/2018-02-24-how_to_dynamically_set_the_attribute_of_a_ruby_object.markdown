---
layout: post
title:      "How to Dynamically Set the Attribute of a Ruby Object"
date:       2018-02-24 23:32:30 +0000
permalink:  how_to_dynamically_set_the_attribute_of_a_ruby_object
---


Updating an object's attribute in Ruby is fairly simple.  Assuming that the attribute is listed under the object's attr_accessor or has a custom setter, it can be simple as:

     car.color = 'red'

However, what if an object has a couple dozen attributes? Writing a setter method for every one of those attributes would be impractical and not very efficient.  And one cannot just chain a variable holding the attribute name to the object and expect that to output the desired result.

There are a couple instance methods that can take in as arguments, the name of the attribute and its new value, and apply it to the instance by invoking that attribute as a method to update the desired instance's attribute.

**#instance_variable_set** | https://apidock.com/ruby/Object/instance_variable_set

```
attribute = "@#{name}".to_sym
your_object.instance_variable_set(attribute, value)

or

your_object.instance_variable_set(:@attribute, 'value')
```

**#send ** | [https://apidock.com/ruby/Object/send](https://apidock.com/ruby/Object/send)

`your_obj.send("#{attribute}=", attribute)`
