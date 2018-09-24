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
}
