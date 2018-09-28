---
layout: post
title: "Effective C++"
date: 2018-09-19
categories: [Languages]
tags: [c++, program]
use_math: true
---

## Item 1: View C++ as a federation of languages
All the "proper usage" rules seem to have exceptions. How are we to make
sense of such a language?

The easiest way is to view C++ not as a single language but as a federation 
of related languages. Within a particular sublanguage, the rules tend to be
simple, straightforward, and easy to remember. 
1. C
1. Object-oriented C++
1. Template C++
1. The STL

Keep these four sublanguages in mind, and don't be surprised when you
encounter situations where effective programming requires that you change
strategy when you switch from one sublanguage to another.

## Item 2: Prefer consts, enums, and inlines to #defines

## Item 3: Use const whenever possible

If the word const appears to the left of the asterisk, what's 
pointed to is constant; if the word const appears to the right of the
asterisk, the pointer itself is constant; if const appears on both sides,
both are constant.

const Member Functions

## Item 4: Make sure that objects are initialized before they're used

The rules of C++ stipulate that data members of an object are initialized
before the body of a constructor is entered. (to use the member
initialization list instead of assignments)

For objects of built-in type, there is no difference in cost between
initialization and assignment, but for consistency, it's often best to
initialize everything via member initialization.

Sometimes the initialization list must be used, even for built-in types. For
example, data members that are const or are references must be initialized;
they can't be assigned.

To avoid using objects before they're initialized, then, you need to do only
three things. First, manually 
initialize non-member objects of built-in types. Second, use member
initialization lists to initialize all parts 
of an object. Finally, design around the initialization order uncertainty
that afflicts non-local static objects defined in separate translation
units.

Chapter 2. Constructors, Destructors, and Assignment Operators

## Item 5: Know what functions C++ silently writes and calls

## Item 6: Explicitly disallow the use of compiler-generated functions you do not want

By declaring a member function explicitly, you prevent compilers from
generating their own version, and by
making the function private, you keep people from calling it.

The scheme isn't foolproof, because member and friend functions can still
call your private functions.

Declaring member functions private and deliberately not implementing them is
the way.

To disallow functionality automatically provided by compilers, declare the
corresponding member functions private and give no implementations. Using
a base class like Uncopyable is one way to do this.

```cpp
class Uncopyable
{
    protected:
        Uncopyable(){}
        ~Uncopyable(){}
    private:
        Uncopyable(const Uncopyable&);
        Uncopyable& operator=(const Uncopyable&);
};
```

## Item 7: Declare destructors virtual in polymorphic base classes

C++ specifies that when a derived class object is deleted through a pointer 
to a base class with a non-virtual destructor, results are undefined. 
What typically happens at runtime is that the derived part of the object is
never destroyed.

Eliminating the problem is simple: give the base class a virtual destructor.
Then deleting a derived class object will do exactly what you want.

When a class is not intended to be a base class, making the destructor
virtual is usually a bad idea.

The implementation of virtual functions requires that objects carry
information that can be used at runtime
to determine which virtual functions should be invoked on the object. This
information typically takes the
form of a pointer called a vptr ("virtual table pointer"). 

Declare a virtual destructor in a class if and only if that class contains
at least one virtual function

If you're ever tempted to inherit from a standard container or any other
class with a non-virtual destructor, resist the temptation! 

Classes not designed to be base classes or not designed to be used
polymorphically should not declare virtual destructors.

## Item 8: Prevent exceptions from leaving destructors
Destructors should never emit exceptions. If functions called in a destructor
may throw, the destructor should catch any exceptions, then swallow them or
terminate the program.

If class clients need to be able to react to exceptions thrown during an
operation, the class should provide a regular (i.e., non-destructor) function
that performs the operation.

If an operation may fail by throwing an exception and there may be a need to
handle that exception, the exception has to come from some non-destructor
function.

## Item 9: Never call virtual functions during construction or destruction
During base class construction of a derived class object, the
type of the object is that of the base class. Not only do virtual functions
resolve to the base class, but the parts of the language using runtime
type information treat the object as a base class type. 

The same reasoning applies during destruction. Once a derived class
destructor has run, the object's
derived class data members assume undefined values, so C++ treats them
as if they no longer exist.
Upon entry to the base class destructor, the object becomes a base class
object, and all parts of C++ virtual functions, dynamic_casts, etc.,
treat it that way.

Since you can't use virtual functions to call down from base classes during
construction, you can compensate by having derived classes pass necessary
construction information up to base class constructors instead. 

## Item 10: Have assignment operators return a reference to \*this

## Item 11: Handle assignment to self in operator=
