# IBM 31SD Control Card Reverse Engineering

The IBM 31SD is a 1970s 8 inch floppy drive that was used in several different systems of theirs, including the IBM 3274-51C (and -52C) terminal controller and the IBM 5280 Distributed Data System.

It has a small circuit board with some analog circuitry for reading and writing data as well as controlling the head load solenoid and head stepper motor.

![31SD Control Card](https://github.com/schlae/IBM31SD/blob/main/photos/31SDControlCard.jpg)

The circuit board is partially documented in the following sources:

[IBM 3270 Control Unit Models 51C and 52C Maintenance Concepts](http://www.bitsavers.org/pdf/ibm/3274/SY27-2528-2_3274_Contol_Unit_Models_51C_and_52C_Maintenance_Concepts_Feb81.pdf) - This document contains a block diagram of the card on PDF page 170.

[IBM 5280 Distributed Data System Diskette Drive Maintenance Manual](http://bitsavers.trailing-edge.com/pdf/ibm/5280/ce/SY31-0602-0_5280_Diskette_Drive_MIM_Mar80.pdf) - This document is less useful and contains mostly duplicate information, although the block diagram is missing.

Unfortunately there is no schematic, and the parts only have seven-digit IBM internal part numbers. There are partial lists of these part numbers on the internet in various places, but most of the parts on this board have no documentation whatsoever.

In the off-chance that someone might find this useful, I've completely reverse engineered the card and documented information about the IBM part numbers.

See the [schematic PDF](https://github.com/schlae/IBM31SD/blob/main/IBM31SD.pdf).

## IBM part numbers

Here is a list of IBM part numbers on this board along with information about each. I have not included physical locations or designators but they can be implied from the schematic.

A quick note about IBM part numbers: They are often divided into a group of three numbers and a group of four numbers with a space in between. Some components truncate the part number, showing only the last 3, 4, or 5 digits.

| IBM part number | Description |
| --------------- | ----------- |
| *Integrated circuits* | |
| 2392100 | Equivalent to a TTL 7400 NAND gate. |
| 2392102 | Equivalent to a TTL 7404 inverter. |
| 1582979   | Marked "2979". Equivalent to an MC1472 NAND driver. |
| 2396475 | Equivalent to a uA723 (or LM723) voltage regulator (in 10-pin TO-100).|
| 5616846 | Detector. This converts filtered analog disk data into digital flux transitions. |
| 5616847 | Amplifier-differentiator. This amplifies the analog head signal and differentiates it. |
| 5897738 | Preamp. This amplifies the read signal from the head or, when in write mode, drives pulses into the head. |
| *Resistor arrays (RPAKs)* | |
| 2392471 | 4-pin, 3 resistor, each 90 ohms. Pin 1 is the common pin. |
| 2392488 | 4-pin, 3 resistor, each 400 ohms. Pin 1 is the common pin. |
| 2392787 | 6-pin, 4 resistor, each 1K. Resistors on pins 1 and 2 are bussed to pin 3, and resistors on pins 5 and 6 are bussed to pin 4. |
| 2408334 | 4-pin, 2 resistor, each 120K ohms. Pins 1 and 2 is one resistor, pins 3 and 4 are the other resistor. |
| 2408846 | 8-pin, 2 resistor, each 95 ohms. Pins 1 and 4 is one resistor, pins 5 and 8 are the other resistor. Presumably this resistor can handle higher power levels. |
| *Tantalum capacitors* | |
| 1589440 | Marked "440". Probably 1uF with a voltage rating of at least 35V. |
| 2396951 | Marked "951". Probably 10uF with a voltage rating probably less than 10V. |
| 5616808 | Marked "808". Probably 4.7uF with a voltage rating probably less than 10V. |
| *Ceramic capacitors* | |
| 1539475 | Marked "9475". 0.1uF, unknown voltage rating. |
| 1589422 | Marked "9422". 0.01uF, unknown voltage rating. |
| 2391271 | Marked "1271". 120pF, unknown voltage rating. |
| 5616796 | Marked "6796". 68pF, unknown voltage rating. |
| 5616797 | Marked "6797". 180pF, unknown voltage rating. |

I'm less certain about part numbers for other devices on this board:

* Red axial film capacitor marked "491 309 123 8210" which may contain a part number and a date code. It measures out to 2700pF.
* Diode, glass package, marked 66 234 GG with a Fairchild logo.
* Diode, rectifier, marked G1419U.
* Transistor, probably NPN, marked 194 U8227K. The important bit is the "194" and the rest is a date code. It has a Motorola logo.
* Transistor, probably PNP, marked 131 U 213H. The important bit is the "131" and the rest is a date code. It has what appears to be a Fairchild logo.

