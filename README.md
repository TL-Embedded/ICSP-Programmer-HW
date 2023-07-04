# ICSP-Programmer-HW

This is a ICSP programming board for AVR targets.

The processor onboard is an ATMEGA8A, and can be programmed using another ICSP-Programmer.

# Connector

The connector is laid out as per a standard Arduino ICSP programmer, so this can to program AVR Arduinos via IDC ribbon cable. This can also be combined with a TC2030 cable for a tag connect solution.

The ICSP connector is laid out as follows:

| Function | Pin # | Pin # | Function |
| -------- | ----- | ----- | -------- |
| MISO     | 1     | 2     | VCC      |
| SCK      | 3     | 4     | MOSI     |
| NRST     | 5     | 6     | GND      |

# Target VCC

The programmer powered via 5V from USB, but does **not** power the target by default. The `VCC` pin is used for voltage reference. The target voltage may be anywhere between 1.8V and 5.5V.

The labeled `VCC` pin can be used to inject voltage to the target. Alternately the jumper `JP1` can be shorted to tie `VCC` to USB 5V.

# USB

The USB C connector operates in USB 2.0 legacy mode. A FTDI `FT230QX` chip provides a serial port interface.

Drivers for the FTDI chip can be found [here](https://ftdichip.com/drivers/).

# Software

The [avrdude](https://github.com/avrdudes/avrdude) command line is the reccommended way to use this programmer.

