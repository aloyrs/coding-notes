all c++ programs must have a main() function

# Comments

```cpp
// Single line comment

/* This is a multi-line comment.
   This line will be ignored.
   So will this one. */
```

# Initialization

```cpp
double d = 1.7789856453427678;
int a{d}; //Compile time error - value of d will not fit in a
int a(d); //ok - a is 1
int a = d; //ok - a is 1
```

Why so many ways of initialization?

It is an historical question. The first one is int i=0;. This one is from the early C language from the 1970's.

Next first C++ versions introduced a function like initialization syntax which writes here int i(0);.

But because of the most vexing parse ambiguities, the curly braces initialization was invented.

And for compatibility reasons, all those syntaxes are still valid...

https://stackoverflow.com/questions/62756177/why-have-different-ways-of-variable-initialization-in-c
