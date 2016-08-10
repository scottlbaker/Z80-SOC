
## Summary

This project is an SOC (System on a Chip) coded in VHDL and implemented for the Lattice iCE40-hx8k dev board. The SOC contains the following components: Z80 CPU + UART + Timer + I/O Ports

## Required Hardware

* Lattice iCE40-hx8k dev board (can be ordered online at www.latticesemi.com)
* USB-to-Serial 3.3V adapter (can be ordered from eBay)
* misc USB cables and wires for connecting the USB-to-Serial adapter

NOTE: Make sure the USB-to-serial adapter is a 3.3V version. Some adapters have 5V interface signals which could damage your iCE40-hx8k dev board.

## Tools

* IceCube2 (from Lattice Semiconductor) was used for synthesis and FPGA Routing.
* Icestorm (https:/github.com/cliffordwolf/icestorm) was used for programming.


## Build Flow

I used the Lattice IceCube2 software to generate the SOC_bitmap.bin programming file and then I used this command line "iceprog SOC_bitmap.bin" the program the iCE40-hx8k dev board over the USB cable (iceprog is part of the icestorm tool suite).

## Console Interface

I used the minicom program (on Ubuntu Linux) as a console to communicate with the Z80 SOC over the USB-to-Serial connection. Configure minicom using the command line "minicom -s" to configure the serial port for ttyUSB0 and turn of the hardware handshaking. There are probably other alternatives to minicom. Any ANSI terminal-emulator program should work for this application.

## Pinout

The iCE40 pins are defined as follows:
```
UART_RXD   G1 -pullup yes
UART_TXD   G2
PORTA[0]   B5
PORTA[1]   B4
PORTA[2]   A2
PORTA[3]   A1
PORTA[4]   C5
PORTA[5]   C4
PORTA[6]   B3
PORTA[7]   C3
RESET      N3 -pullup yes
CLK        J3 -pullup yes
```

## Memory Map

The memory map of this SOC is as follows:
```
0 -> 0fff  4k bytes of RAM
```

## I/O Map

The I/O map of this SOC is as follows:
```
00 -> 07   UART  registers
08 -> 0b   Timer registers
0c         Output register
0d         Interrupt mask register
0e -> 0f   Random number generator
10         Interrupt source register
```

## Z80 CPU Background Info

The Zilog Z-80 was introduced in July of 1976. Two key engineers at Zilog (Federico Faggin and Masatoshi Shima) were former Intel engineers and they designed the Z80 to be a backward-compatible enhancement to the Intel 8080 design. The Z80 could execute all 8080 opcodes, and also included additional opcodes for bit manipulation, shifts and rotates on memory and registers other than the accumulator, program looping, block move, block (I/O), and byte search. The Z80 had 2 copies of the register set that could be switched to allowed fast operating system or interrupt context switches. It also added two 16-bit index registers (IX and IY) and two types of relocatable vectored interrupts (direct or via the 8-bit I register).

## Contributors

* Scott L Baker - SOC design

## License

See the **LICENSE** file in this repository
