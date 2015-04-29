# Introduction #

Many people have the misconception that C++ is bloated and not fit for small embedded devices. However, C++ is a very broad language and the efficiency of the output is heavily dependent on the code written.

# Why C++ at all? #

C++ provides many advantages in coding style and organization:
  * Namespaces
  * Templated functions (use carefully!)
  * Classes
  * That fun little `::` syntax all over the place

Also... _just because I wanted to_. If anything else, I started writing this library in C++ for a few personal reasons:
  * To learn the repercussions of using C++ compared to C in embedded devices
  * To get a deep understanding of the byte-level output of compiled C++ code
  * Because I like to create elegant code, and C++ allows me to do that better than C

## But aren't classes bloated and expensive? ##

This is completely dependent on how you use them. In their simplest form (no virtual functions, no inheritance), classes are simply a programming construct to organize:
  * A set of associated variables (which comprises an 'object')
  * A set of related functions

In general, a call to an object's method:
```
 object.method(var1, var2);
```

Can be thought of as a C function call like:
```
 method(&object, var1, var2);
```

## Don't templated functions/classes produce lots of code? ##
Yes, they can! Be careful when using templates, as the compiler may not be able to remove duplicated functionality.

For instance, if two different C++ files get compiled that have the same instantiation of a templated function, that function's byte-code can be duplicated in the final product binary.

# What do I lose by going to C++? #
There are only two drawbacks that I have found:
  1. A small amount of bloat in very special situations
  1. No [designated initializers](http://gcc.gnu.org/onlinedocs/gcc/Designated-Inits.html) in C (when using C99).

# I still think your an idiot #
A) It's "you're". Secondly, leave a comment and explain why!