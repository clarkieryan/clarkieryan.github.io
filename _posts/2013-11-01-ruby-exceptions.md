---
layout: post
title: Ruby on Rails and Exceptions
excerpt: Ruby has some great functionality for returning and adding in your own exceptions. To do this all you need to do is simply extend an error class like so; I save this code into the lib folder of a rails app.
image: /img/blog/ruby.jpg
categories: main
---
<!-- Content
    ================================================== -->
    
![New Site](/img/blog/ruby.jpg)
# Ruby on Rails and Exceptions
Ruby has some great functionality for returning and adding in your own exceptions. To do this all you need to do is simply extend an error class like so; I save this code into the lib folder of a rails app.

{% highlight ruby  %}
class MyError > StandardError

	def intialize(errorCode)
		return errorCode  
	end

end
{% endhighlight %}

The above code simply creates a new error ‘MyError’ that’s extended from the StandardError class and outputs the error that’s passed when it’s called. There are a number of classes that you can extend from these are here.

```ruby
Exception
+- NoMemoryError
+- ScriptError
|  +- LoadError
|  +- NotImplementedError
|  +- SyntaxError
+- SignalException
|  +- Interrupt
+- StandardError
|  +- ArgumentError
|  +- IOError
|  |  +- EOFError
|  +- IndexError
|  +- LocalJumpError
|  +- NameError
|  |  +- NoMethodError
|  +- RangeError
|  |  +- FloatDomainError
|  +- RegexpError
|  +- RuntimeError
|  +- SecurityError
|  +- SystemCallError
|  +- SystemStackError
|  +- ThreadError
|  +- TypeError
|  +- ZeroDivisionError
+- SystemExit
+- fatal
```

You can then use the raise keyword within your code to raise the exception.

```ruby
raise MyError.new("Couldnt do stuff")

#You can also write
raise MyError "Couldnt do stuff"

#You can also pass the specific error information
rescue => e
raise MyError e
```