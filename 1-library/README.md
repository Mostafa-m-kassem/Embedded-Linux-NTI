# Library

A library constitutes a collection of pre-compiled functions aimed at preventing code redundancy, which is encapsulated within a package termed a library.

Note: A library isn't executable.

## Static Library and Compilation Process

### Overview

A **static library** comprises object files that undergo linking during the compilation phase of a program. Unlike dynamic libraries, static libraries integrate with the program during compile time, resulting in a unified executable file containing both program and library code.

### Compiling a Static Library

#### 1. Crafting Your Code

Begin by composing the source code for your library. For instance, let's construct a simple library dubbed `mylib` housing a function called `add_numbers`:

```c
#ifndef MYLIB_H
#define MYLIB_H

int add_numbers(int a, int b);

#endif
```

```c
#include "mylib.h"

int add_numbers(int a, int b) {
    return a + b;
}
```

#### 2. Compilation of Source Files

Compile the source files (e.g., `mylib.c`) into object files using a compiler such as `gcc`:

```bash
gcc -c mylib.c -o mylib.o
```

#### 3. Creating the Static Library

Utilize the `ar` (archiver) command to craft the static library (`libmylib.a`):

```bash
ar rcs libmylib.a mylib.o
```

This command fabricates a static library (`libmylib.a`) and incorporates the object file (`mylib.o`) into it.

#### 4. Integrating the Static Library into Your Program

Now, incorporate the static library into your main program. Develop a program (`main.c`) that includes the library header and invokes the library function:

```c
// main.c
#include <stdio.h>
#include "mylib.h"

int main() {
    int result = add_numbers(5, 7);
    printf("Result: %d\n", result);
    return 0;
}
```

#### 5. Compiling Your Program with the Static Library

Compile your program with the static library:

```bash
gcc main.c -o my_program -L. -lmylib
# OR
gcc main.c -o my_program -L. libmylib
```

Here, `-L.` instructs the linker to search for libraries in the current directory, and `-lmylib` links your program with `libmylib.a`.

#### 6. Executing Your Program

Execute the compiled program:

```bash
./my_program
```

## Dynamic Library and Compilation Process

### Overview

A **dynamic library** encompasses compiled code that can be loaded into a program during runtime. Differing from static libraries, dynamic libraries aren't embedded into the executable during compile time. Instead, they link at runtime, furnishing programs with flexibility and modularity.

### Compilation of a Dynamic Library

#### 1. Crafting Your Code

Similar to static libraries, compose the source code for your library. For example, let's fabricate a dynamic library named `mylib` with a function named `add_numbers`:

```c
// mylib.h
#ifndef MYLIB_H
#define MYLIB_H

int add_numbers(int a, int b);

#endif
```

```c
// mylib.c
#include "mylib.h"

int add_numbers(int a, int b) {
    return a + b;
}
```

#### 2. Compiling the Dynamic Library

Compile the source file into a shared object (dynamic library) using the `-shared` flag:

```bash
gcc -shared -fPIC -o libmylib.so mylib.c
```

The `-shared` flag signifies the creation of a shared object, while `-fPIC` generates position-independent code, essential for shared libraries.

#### 3. Integrating the Dynamic Library into Your Program

Develop a program (`main.c`) that includes the library header and invokes the library function:

```c
// main.c
#include <stdio.h>
#include "mylib.h"

int main() {
    int result = add_numbers(5, 7);
    printf("Result: %d\n", result);
    return 0;
}
```

#### 4. Compiling Your Program with the Dynamic Library

Compile your program with the dynamic library:

```
gcc main.c -o my_program -L. -lmylib
```

Here, `-L.` directs the linker to search for libraries in the current directory, and `-lmylib` links your program with `libmylib.so`.

#### 5. Executing Your Program

Execute the compiled program:

```bash
./my_program
``` 

