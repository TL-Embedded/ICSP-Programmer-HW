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

# Firmware

The firmware for this PCB is [ICSP-FW.hex](./firmware/ICSP-FW.hex).
See the usage section for an example of programming a ICSP programmer from another programmer.

Note: To Program a ICSP programmer, its target `VCC` must *not* be powered. Ensure that `JP1` is open, and no power is provided via the `VCC` pin or ICSP connector.

# Usage

The windows executable version of [avrdude](https://github.com/avrdudes/avrdude) is included in this repo to flash a target.

You will need to substitute your serial port and target information.

An example for flashing the ICSP firmware is below:
```sh
# Verify the target is connected.
.\avrdude.exe -C "avrdude.conf" -c avrisp -P COM3 -b 115200 -p ATMEGA8

# Configure the target fuses.
# This is required to set the oscillator config
.\avrdude.exe -C "avrdude.conf" -c avrisp -P COM3 -b 115200 -p ATMEGA8 -U lfuse:w:0xbe:m -U hfuse:w:0xd9:m

# Flash the target with 'ICSP-FW.hex'
.\avrdude.exe -C "avrdude.conf" -c avrisp -P COM3 -b 115200 -p ATMEGA8 -U flash:w:ICSP-FW.hex:i
```
