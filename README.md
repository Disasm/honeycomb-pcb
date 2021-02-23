# honeycomb

An experimental board with GW1NS-2C FPGA.

## Programming

To program the board you need [openFPGALoader](https://github.com/trabucayre/openFPGALoader).

SRAM programming:

```
openFPGALoader -b littleBee -c ft2232 bitstream.fs
```

Internal flash programming:

```
openFPGALoader -b littleBee -c ft2232 -f bitstream.fs
```

## JTAG interface firmware update

To update the firmware you need to reboot into a bootloader:
* Disconnect the board from USB and power supplies.
* Short 3.3V line and the first pin of the STM32F042 MCU.
* While shorting the pin, connect a USB cable.

Then update the firmware with dfu-util:

```
dfu-util -a 0 -s 0x08000000:leave -D firmware.bin
```

## Revision History

### 1.0: 2021-02-19

* First version.
* Errata:
    * 3.3V supply should be used for VCCX instead of 1.8V supply.
    * Power LED is too bright.
    * Resistor values on a schematic do not correspond to the available values.
