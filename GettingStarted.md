

# Introduction #

SAVR is designed to be a cross-micro C++ library for the Atmel AVR 8-bit family.

This has been a growing collection of code over many years. After reaching a substantial size, and finding that it was (at least somewhat) useful to others that I knew, I decided it was best to host the code publicly for all.

# Compiling the Library #

## Requirements ##
This has been tested and built with GCC for AVR. The only pre-packaged systems used/supported are WinAVR for Windows, and CrossPack for OS X.

The makefile creates a static library named "libsavr`_`MCU`_`SPEED.a". For the most common Arduinos, this will be "libsavr`_`atmega328p`_`16000000.a".

## Building ##
Command line:
  1. CD to the lib/ directory
  1. Run something like "make MCU=atmega328p F`_`CPU=16000000"
  * Substitute the MCU with whatever you will be using (the GCC supported target for -mmcu=xxxx)
  * Substitute the CPU clock speed with your target's speed
  * If your MCU isn't supported by my library, let me know, or better yet, create a patch!

Eclipse:
  1. Create a "Makefile project with existing code"
  1. Make the existing code location be the root of the Git repository
  1. Go into the project properties
  1. Find "C/C++ Build"
  1. Uncheck "Use default build command"
  1. Modify the build command to be "make -C lib MCU=atmega328p F`_`CPU=16000000"
  * Again, change the MCU and frequency accordingly


# Linking to the Library #
Test projects are included under the tests/ directory. This also has a Test.mk makefile which shows how I normally build.

This is no different than linking against any other library. In this case, use "-lsavr`_`MCU`_`SPEED" at the linking stage. For instance, "-lsavr`_`atmega328p`_`16000000"

# Using the Library #

## Including the header files ##
I recommend adding the include/ folder to the include path when compiling. That way you can limit header file naming collision and match the style used by the library itself and the tests provided. Including SAVR header files should look like:
```
#include <savr/w1.h>
#include <savr/dstherm.h>
...
```

## Code organization ##
The library is grouped into either classes or namespaces. Namespaces are used in situations where there is no need for multiple objects (for instance, a single terminal, a single UART for stdin/stdout binding, etc).

## Frequency dependence ##
Version 0.3 was compile-time frequency independent, meaning that the actual clock frequency needed to be passed in to many constructors or initializers. This was for a grand idea that you could possibly change the system clock on the fly with an external PLL or oscillator. Coding like this for the one guy who might actually end up doing this, it wasn't worth it -- the code was getting too bloated and too heavy. This independence was removed in version 1.0, and the library is now compiled for a specific target frequency. The code optimization allows for it to run on smaller, slower devices.


## Global objects ##
There is no 'new' or 'delete' support. This means all objects must be globally created using static initialization, or have a global pointer to a persistent stack object.

Static initialization:
```
static W1 wire(GPIO::C0);

...

foo() {
    wire.Reset();
    ...
}
```

Global pointer to persistent object:

```
static W1 *wire;

...

foo() {
    wire->Reset();
    ...
}

...

int main(void) {
    W1 localWire(GPIO::C0);
    wire = &localWire;

    ...

    while(1) {
        ...
    }
}
```