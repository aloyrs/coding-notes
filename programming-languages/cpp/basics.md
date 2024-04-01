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

# Printing

## `std::cout`

`<<` is a insertion operator

```cpp
#include <iostream> // for std::cout

int main()
{
    int x{ 5 };
    std::cout << "x is equal to: " << x;
    return 0;
}

// x is equal to: 5
```

## `std::endl` vs `\n`

std::endl ❌

```cpp
std::cout << "Hi!" << std::endl; // std::endl will cause the cursor to move to the next line of the console
std::cout << "My name is Alex." << std::endl;

// Hi!
// My name is Alex.
```

Prefer `'\n'` over `std::endl` when outputting text to the console because `std::end` moves cursor to next line + flushes buffer

`\n` ✅

```cpp
std::cout << "x is equal to: " << x << '\n';
std::cout << "And that's all, folks!\n";
```

## Buffering & flushing

`std::cout` is buffered , meaning a buffer stores all cout until it is full then it will print the output all together into the terminal. increase efficiency as less operations to terminal.

Use `std::flush` to manually flush out the buffer to ensure immediate display
