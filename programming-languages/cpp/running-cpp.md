# How C++ source code is compiled

.cpp files compiled into .o files

linker links .o + other library files into .exe files

# How to run C++

- Install C++ compiler
- Write C++ source code

```cpp
#include <iostream>

int main()
{
    std::cout << "Hello World" << std::endl;
}
```

- Go to terminal and cd to path of .cpp file
- Compile cpp code to exe using g++ compiler

```bash
g++ -o Helloworld .\helloworld.cpp
```

- Run the `Helloworld.exe` file with :

```bash
./Helloworld
```
