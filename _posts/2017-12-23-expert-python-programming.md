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

![implementation of custom metaclasses]({{ "/assets/imgs/metaclasses.png" | absolute_url }})

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
