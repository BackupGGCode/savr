A C++ library for a handful of different AVR microcontrollers. This is primarily developed on the Arduino, but modified to be cross-platform (cross-micro) to other AVRs I have laying around.

The current release is SAVR 1.2. To get a copy of the savr library, use Git: git clone https://code.google.com/p/savr/

Library includes:
  * Pin-based GPIO interface
  * Interfaces for various buses:
    * SPI
    * SCI (UART)
    * TWI (I2C)
    * 1-Wire
  * SCI/UART binding to stdin and stdout
  * Terminal interface
    * Simple command interface
    * Keeps track of command history with up/down arrow navigation
  * Various Peripherals:
    * ST7066/HD44780 based character LCDs
    * W5100 (Arduino ethernet shield, not fully developed)
    * SD Cards over SPI
    * DS18B2x and DS182x 1-Wire temp sensors

The library has been at least somewhat tested with the following:
  * ATmega328P (Arduino)
  * ATmega8
  * ATmega88
  * ATmega8515
  * ATmega16
  * ATmega32
  * ATmega644P

Variants to the devices listed above, if they share the same specification document, are also considered as supported. For instance, the ATmega48, 88, and 168. Adding support for new devices is usually trivial.

The SAVR library compiles for nearly every AVR that's supported by GCC<span title="OK, so I have no data to back that up. I think that's the case, and it sure does sound good, right?"><sup>[+]</sup></span>. There are some micro-specific sections that rely on knowledge of the exact AVR in use, such as the SCI, SPI, and TWI interfaces. If the target micro isn't known to the SAVR library, those sections will be removed.

This library relies on avr-libc and AVR GCC, such as distributed through WinAVR and CrossPack for AVR.