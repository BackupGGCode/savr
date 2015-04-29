The SAVR library compiles for nearly every AVR that's supported by GCC<span title="OK, so I have no data to back that up. I think that's the case, and it sure does sound good, right?"><sup>[+]</sup></span>. There are some micro-specific sections that rely on knowledge of the exact AVR in use, such as the SCI, SPI, and TWI interfaces. If the target micro isn't known to the SAVR library, those sections will be removed. This is mostly due to varying naming conventions used by Atmel across different lines, which is propagated into avr-libc. This library tries to commonize the names of registers and bit values used in the code.

# Hardware Tested Devices #
The library has been tested with hardware in the loop (HIL) for:
  * ATmega328P (Arduino)
  * ATmega8
  * ATmega88
  * ATmega8515
  * ATmega16
  * ATmega32
  * ATmega644P

# Compilation Support #
In addition to HIL testing many additional micros have been "compile tested". That is, I've just made sure that the compilation doesn't fail. The following are the names specified to GCC with `-mmcu=`:
  * atmega8
  * atmega16
  * atmega32
  * atmega644
  * atmega8515
  * atmega48
  * atmega88
  * atmega168
  * atmega48p
  * atmega88p
  * atmega168p
  * atmega88pa
  * atmega328p
  * atmega164p
  * atmega324p
  * atmega644p
  * atmega164a
  * atmega324a
  * atmega324pa
  * atmega644a
  * atmega644pa
  * atmega1284p