---
layout: post
title:  "expert python programming"
date:   2017-12-23
categories: [LANGUAGES]
mathjax: true
---
## Current Status of Python
### The popular tools and techniques used for maintaining cross-version
compatibility

The best way so far to define how compatibility may change in the future is
by the proper approach to versioning numbers using Semantic Versioning      
(http://semver.org/), or shortly, semver. 

Given a version number MAJOR.MINOR.PATCH, increment:
* A MAJOR version when you make incompatible API changes
* A MINOR version when you add functionality in a backwards-compatible
manner
* A PATCH version when you make backwards-compatible bug fixes The benefit
of using projects that follow semver is that usually what needs to be tested
are only major releases because minor and patch releases are guaranteed not 
to include backwards incompatible changes. This is only true if such
projects can be trusted not to break such a contract.

### Popular productivity tools

## Syntax Best Practices - below the Class Level
### dictionary implementation details
CPython uses hash tables with pseudo-random probing as an underlying data
structure for dictionaries. Due to this implementation detail, only objects
that are hashable can be used as a dictionary key. An object is hashable if it
has a hash value that never changes during its lifetime and can be compared
to different objects. 

Two objects that are compared equal must have the same hash value. The reverse
does not need to be true. This means collisions of hashes are possible—two
objects with the same hash may not be equal. 

### Advanced syntax
#### Iterators
An iterator is nothing more than a container object that implements the
iterator protocol. It is based on two methods:
* \_\_next\_\_: This returns the next item of the container
* \_\_iter\_\_: This returns the iterator itself

#### Generators
Generators provide an elegant way to write simple and efficient code for
functions that return a sequence of elements. Based on the yield statement,
they allow you to pause a function and return an intermediate result. The
function saves its execution context and can be resumed later, if necessary.

#### Decorators
Decorators were added in Python to make function and method wrapping (a
function that receives a function and returns an enhanced one) easier to
read and understand. 

The decorator is generally a named object (lambda expressions are not
allowed) that accepts a single argument when called (it will be the 
decorated function)
and returns another callable object. "Callable" is used here instead of
"function" with premeditation. While decorators are often discussed in the
scope of methods and functions, they are not limited to them. In fact,
anything that is callable (any object that implements the `__call__` method
is considered callable), can be used as a
decorator and often objects returned by them are not simple functions but
more instances of more complex classes implementing their own `__call__` 
method.

The generic patterns is as follows:

Common pitfalls of using decorators is not preserving function metadata
(mostly docstring and original name) when using decorators.

## Syntax Best Practices --- above the Class Level
### Subclassing built-in types
### Accessing methods from superclasses
The shorter form of super (without passing any arguments) is allowed inside
the methods but super is not limited to methods. 
When only the first argument is provided, then super returns an unbounded
type. This is especially useful when working with classmethod.
### Old-style classes and super in Python 2
Python 3 no longer maintains the concept of old-style classes, so any class
that does not inherit from any other class implicitly inherits from object. 
### Understanding Python's Method Resolution Order
Python's Method Resolution Order is based on *C3*, the MRO built for the Dylan
programming language.
### Descriptors
A descriptor lets you customize what should be done when you refer to an
attribute on an object.
#### Real-life example – lazily evaluated attributes
One example usage of descriptors may be to delay initialization of the class
attribute to the moment when it is accessed from the instance. 
#### Properties
The properties provide a built-in descriptor type that knows how to link an
attribute to a set of methods. A property takes four optional arguments: fget,
fset, fdel, and doc. 
### Metaprogramming
> "Metaprogramming is a technique of writing computer programs that can
> treat themselves as data, so you can introspect, generate, and/or modify
> itself while running."
Using this definition, we can distinguish two major approaches to
metaprogramming in Python.

The first approach concentrates on the language's ability to introspect its
basic elements such as functions, classes, or types and to create or modify
them on the fly.
Next are special methods of classes that allow you to interfere with class
instance process creation.
#### Decorators – a method of metaprogramming
#### Class decorators
The only difference is that they are expected to return a class instead of the
function object. 
### Metaclasses
Metaclass is a type (class) that defines other types (classes). 

The most important thing to know in order to understand how they work is
that classes that define object instances are objects too. So, if they are
objects, then they have an associated class. 

The basic type of every class definition is simply the built-in type class.
In Python, it is possible to substitute the metaclass for a class object
with our own type.

![implementation of custom metaclasses]({{ site.url }}/assets/metaclasses.png)

Every class created with the class statement implicitly uses type as its
metaclass. This default behavior can be changed by providing the metaclass
keyword argument to the class statement.
{% highlight python %}
    class ClassWithAMetaclass(metaclass=type):
        pass
{% endhighlight %}
The value provided as a _metaclass_ argument is a metaclass argument is
usually another class object, but it can be any other callable that accepts
the same arguments as the _type_ class and is expected to return another
class object. 
The call signature is `type(name, bases, namespace)`, which is explained as
follows:
*  _name_: This is the name of class that will be stored in the 
        `__name__` attribute
*  _bases_: This is the list of parent classes that will become the
        `__bases__` attribute and will be used to construct the MRO of a
        newly created class
*  _namespace_: 

## 4. Choosing Good Names
### Best practices for arguments
In any case, assertions have to be done carefully, and should not be used to
bend Python to a statically typed language. 

### Class names

### Modules and packages
Besides the special module`__init__`, the module names are in lowercase with
no underscores.
When the module is private to the package, a leading underscore is added.

## 5. Writing a Package
The Python Packaging User Guide recommendations of tools for package
creation and distribution are as follows:
* Use setuptools to define projects and create source distributions
* Use wheels in favor of eggs to create built distributions
* Use twine to upload package distributions to PyPI
### Project configuration

### Namespace package
Namespace packages can be understood as a way of grouping related packages
or modules higher than a meta-package level, where each of these packages
can be installed independently.

Namespace packages are especially useful if you have your application
components developed, packaged, and versioned independently but you still
want to access them from the same namespace. 

It is important to know the difference between normal and namespace packages
and what problems they solve.

### Uploading a package

### Standalone executables

## 6. Deploying Code
The process of making a specific version of your application or service
available to the end users is called deployment.

### The Twelve-Factor App
A good source of such practices that encourage building easily deployable
apps is a manifesto called Twelve-Factor App.

As its name says, the Twelve-Factor App consists of 12 rules:

### Deployment automation using Fabric

### Common conventions and practices
The filesystem hierarchy

What really helps is to document conventions for your project.

Isolation

For the purpose of deployments, there is only one important thing to add.
You should always isolate project dependencies for each release of your
application. In practice it means that whenever you deploy a new version of
the application, you should create a new isolated environment for this
release.

Using process supervision tools

Applications on remote servers usually are never expected to quit.
What you need is to have some process supervision tool that can start and
manage your application process.
Two popular tools in the Python community for managing application processes
are Supervisor and Circus.

Application code should be run in user space

Your application code should be always run in user space. This means it must
not be executed under super-user privileges.

The conventional name for a user that owns no files and is in no privileged
groups is nobody, anyway the actual recommendation is to create a separate
user for each application daemon. 

In Linux, processes of the same user can interact with each other, so it is
important to have different applications separated at the user level.

Using reverse HTTP proxies ?????

Reloading processes gracefully

Graceful reloads are today a standard in deploying web applications. 

Code instrumentation and monitoring

To be sure that our product works as expected, we need to properly handle
application logs and monitor the necessary application metrics. 
This often includes:
* Monitoring web application access logs for various HTTP status codes
* A collection of process logs that may contain information about runtime
errors and various warnings
* Monitoring system resources (CPU load, memory, and network traffic) on
remote hosts where the application is run
* Monitoring application-level performance and metrics that are business
performance indicators (customer acquisition, revenue, and so on)

Logging errors – sentry/raven

No matter how precisely your application is tested, the truth is painful.
Your code will eventually fail at some point.
What you can do is be well prepared for such scenarios and make sure that no
error passes unnoticed. 

You could, of course, depend only on such logs stored in files for finding
and monitoring your application errors. Unfortunately, observing errors in
textual logs is quite painful and does not scale well beyond anything more
complex than running code in development.
You will eventually be forced to use some services designed for log
collection and analysis.
What you really need is as much context information about error occurrence
as possible.

Monitoring system and application metrics

Dealing with application logs

While solutions such as Sentry are usually way more powerful than ordinary
textual output stored in files, logs will never die.

Remember that logs are not only about errors. They can be even the core of
the product implementation.

The Twelve-Factor App says that logs should be treated as event streams. So
a log file is not a log per se, but only an output format. 
The fact that they are streams means they represent time ordered events. 

According to the Twelve-Factor App methodology, the application should never
be aware of the format in which logs are stored. This means that writing to 
the file, or log rotation and retention should never be maintained by the
application code. These are the responsibilities of the environment in which
applications are run.

The best conventions for dealing with logs can be closed in a few rules:
* The application should always write logs unbuffered to the standard
output (stdout)
* The execution environment should be responsible for the collection and
routing of logs to the final destination

The main part of the mentioned execution environment is usually some kind of
process supervision tool. 

Both Supervisor and Circus are also capable of handling log rotation and
retention for managed processes but you should really consider whether this 
is a path that you want to go. 
My strong recommendation is to forget about Supervisor's and Circus' log 
rotation capabilities for the sake of consistency with other system
services. logrotate is way more configurable and also supports compression.

## 7. Python Extensions in Other Languages
### Why you might want to use extensions
Improving performance in critical code sections

Integrating existing code written in different languages

Integrating third-party dynamic libraries

Creating custom datatypes

You can, of course, create many custom data structures in Python either by
basing them completely on some built-in types or by building them from
scratch as completely new classes. Unfortunately, for some applications that
may heavily rely on such custom data structures, the performance might not
be enough.

### Writing extensions
Pure C extension

Cython

Cython is both an optimizing static compiler and the name of a programming
language that is a superset of Python. As a compiler, it can perform source 
to source compilation of native Python code and its Cython dialect to Python
C extensions using Python/C API. It allows you to combine the power of
Python and C without the need to manually deal with Python/C API.

For extensions created using Cython, the major advantage you will get is
using the superset language that it provides. Anyway, it is possible to
create extensions from plain Python code using source to source compilation.

Cython sources use a different file extension. It is .pyx instead of .py.

## 8. Managing Code
### Version control systems
### Continuous development processes
There are some processes that can greatly streamline your development and
reduce a time in getting the application ready to be released or deployed to
the production environment. It is important to highlight that they
are strictly technical processes, so they are almost unrelated to project
management technologies, although they can highly dovetail with the latter.

The fact that these are technical processes means that their implementation
strictly depends on the usage of proper tools.

Continuous integration

Continuous integration, often abbreviated as CI, is a process that takes
benefit from automated testing and version control systems to provide a 
fully automatic integration environment. 

Continuous delivery

Continuous delivery is a simple extension of the continuous integration
idea. This approach to software engineering aims to ensure that the
application can be released reliably at any time.

not finished!

## 9. Documenting Your Project
### The seven rules of technical writing
* __Write in two steps:__ Focus on ideas and then on reviewing and shaping
your text.
* __Target the readership:__ Who is going to read it?
* __Use a simple style:__ Keep it straight and simple. Use good grammar.
* __Limit the scope of the information:__ Introduce one concept at a time.
* __Use realistic code examples:__ "Foos" and "bars" should be avoided
* __Use a light but sufficient approach:__ You are not writing a book!
* __Use templates:__ Help the readers to get habits.

### A reStructuredText primer
reStructuredText is also called reST. It is a plain text markup language
widely used in the Python community to document packages.

### Building the documentation

Sphinx

## 10. Test-Driven Development

## 11. Optimization – General Principles and Profiling Techniques
### 11.1 The three rules of optimization
Make it work first

A very common mistake is to try to optimize the code while you are writing
it. As Kent Beck says, "Make it work, then make it right, then make it
fast."

Work from the user's point of view

Remember that optimization has a cost and that the developer's point of view
is meaningless to customers, unless you are writing a framework or a library
and the customer is a developer too.

Keep the code readable and maintainable


