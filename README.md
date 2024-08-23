# 2332/2364 ROM Adapter

This repository provides an adapter for 2332 and 2364 ROMs for vintage computers. With an optional hidden inverter chip on the bottom, all versions of these boards can be emulated. The adapter was designed to have the smallest possible footprint while still using through-hole components for a vintage look. It includes an optional detachable selector board for DIP switches or jumpers. Without the detachable selector board, solder jumpers can be used instead. The provided pads on the bottom allow for synchronized address selection across multiple adapters. The entire project is available under the MIT license.

![Adapter Variations](/Images/InPlace.png)
![Adapter Variations](/Latest/2332_2364_ROM_Adapter_Photo.png)

## Project Details

### Latest Files

In the "Latest" folder, you'll find the most up-to-date design files, including:

- Gerber files suitable for popular online PCB manufacturers like [PCBWay](/Latest/2332_2364_ROM_Adapter_Gerber_PCBWay.zip) and [JLCPCB](/Latest/2332_2364_ROM_Adapter_Gerber_JLCPCB.zip). Most manufacturers should be fine with either.
- A Bill of Materials (BOM) in both [CSV](/Latest/2332_2364_ROM_Adapter_BOM.csv) (with sources) and [PDF](/Latest/2332_2364_ROM_Adapter_BOM.pdf) formats.
- The [full schematics](/Latest/2332_2364_ROM_Adapter_Schematics.pdf) of the adapter.

### Implementation

The adapter has been implemented using KiCAD 7. The KiCAD project files are included in this repository.

![PCB Front](/Latest/2332_2364_ROM_Adapter_3D_Front.png)
![PCB Back](/Latest/2332_2364_ROM_Adapter_3D_Back.png)

### Assembly Instructions

![PCB](/Latest/2332_2364_ROM_Adapter_Photo1.png)

1. Get a straight male pin header with pitch (2.54mm; standard) and break it to a 12-pin length. Do this twice. A machined header is recommended if the adapter will be inserted into a socket. Inserting a square pin in a socket might damage it.
2. Solder the pins in place into the smaller 12-pin lengthwise holes. To align them correctly, you can use another socket or a breadboard. Stick the longer parts into the socket/breadboard and put the PCB on top. Solder first both edges on each. Recheck if they are flush to the header. If not, reheat the corner that needs correction and press down on PCB until flush. Then, solder all other pins.
3. Install the resistor network. One edge has a square around one pin. This should be where pin 1 will be inserted. Pin 1 is identified on the resistor network usually with a dot.
4. Write/burn one of the binaries onto a ROM.
5. (Optional) Solder a socket in place. Similarly to the headers mentioned above, only solder one pin on each side before soldering all to be able to make adjustments as needed. Adding a socket is not recommended for machines which do not have enough clearance for it (e.g., TRS-80 Model 1). For these, you need to skip this step and solder the ROM directly to the board.
6. Solder the ROM to the board or insert it into the socket. Since the pins are close, this might be tricky.

![Partly Assembled](/Latest/2332_2364_ROM_Adapter_Photo2.png)

#### Bank Switching

The adapter allows for bank-switching of various ROMs. Depending on the size of the ROM used, only certain pins may be configurable. For example, a 27256 ROM has 15 address pins. The adapter exposes 13 of these pins to the bottom pins, leaving 2 additional address lines available for bank-switching. A 27512 would then have 3 additional address lines.

**NOTE**: Keep in mind that the bits are active-low. This means that if you want to set a `1` on a specific address, you leave it unbridged. If you want a `0`, you should bridge it. See below for more details on why it was designed this way.

**NOTE**: The board exposes the bits from right to left. If you prefer left to right (e.g., for DIP switches to match labels), you can flip the address bits in the ROM or use the provided "f" versions in the systems ROM repository.

Here are some examples of available bank-switching configurations:

#### No Bank-Switching at all

7. Clip off extension board on perforated line.
8. Use solder bridges on the bottom to pre-select a specific ROM.

![Assembled](/Images/Image4.png)

#### Jumper Caps

7. Add a 2-row pin straight header (2.54mm pitch) to the center two pins of the extension board. Make sure to leave one row of pins on each side—one row on the edge and one next to the ROM.
8. Add jumpers.

#### Right Angle Jumpers

7) Clip off extension board on perforated line.
8) Add a 2 row pin right-angle header (2.54mm pitch) to the bottom of the PCB, extending one end out over the board where the extension was.
9) Add jumpers.

#### DIP Switches

**NOTE**: For the TRS-80 Model 1, use low-profile DIP switches to ensure the adapter fits inside the case.
7) Add a DIP switch to the extension board. The DIP switch should cover all holes from front to back.

![Assembled](/Images/Image2.png)

#### DIP Switches on extension board

7) Clip off the extension board along the perforated line.
8) Solder up to 6 wires (e.g., ribbon cable) to the bottom of the PCB. Use up to 3 wires for each address line, which is the row close to the center of the board. To identify the address lines, refer to the label just below the ROM on the top of the adapter PCB. Solder at least one wire to any of the holes closer to the edge of the board—these are ground pins, so any of them can be used.
9) Solder all wires to the extension board using the central two rows of holes. Solder from the bottom, as the DIP switches will be added to the top. Solder the address lines closest to the perforated line where the extension board was attached to the adapter PCB. Solder the ground wires to the other holes in the second row, further from the perforated edge.
10) Add a DIP switch to the extension board. The DIP switch should cover all holes from front to back. You may need to trim the soldered pins of the cable to allow the DIP switches to sit as close to flush as possible.

![Assembled](/Images/Image3.png)

#### Jumper caps on extension board

7) Clip off the extension board along the perforated line.  
8) Solder up to 6 wires (e.g., ribbon cable) to the bottom of the PCB. Use up to 3 wires for each address line, which is the row close to the center of the board. To identify which address line is which, refer to the label just below the ROM on the top of the adapter PCB. Solder at least one wire to any of the holes closer to the edge of the board—these are ground pins, so any of them can be used.  
9) Add a 2-row pin straight header (2.54mm pitch) to the center two pins of the extension board. Leave one row on each side—one on the edge and one next to the ROM.  
10) Solder all wires to the extension board. Solder the address lines to the row closer to the perforated edge, and solder the single ground wire to the hole at the bottom edge furthest from the perforated edge. You can solder this from either the top or bottom.  
11) Add jumpers.

#### Connect two or more adapters together

![Assembled](/Images/Image1.png)

Sometimes it is useful to be able to bank-switch multiple ROMs simultaneously.

7) Clip off the extension boards on nearly all the boards at the perforated line—except one, which will be used for selection.  
8) Solder up to 6 wires (e.g., ribbon cable) to the bottom of one PCB. Use up to 3 wires for each address line, which is the row close to the center of the board. To identify which address line is which, refer to the label just below the ROM on the top of the adapter PCB. Solder at least one wire to any of the holes closer to the edge of the board—these are ground pins, so any of them can be used.  
9) Repeat the same process for the other board using the other end of the wires. Ensure that the wires from each pad on one adapter connect to the corresponding pad on the other adapter.

![Assembled](/Images/Image5.png)

### Configuration

Depending on which ROM and even the specific version you want to emulate, you will need to configure the adapter accordingly. Below is a list of configurations:

![Assembled](/Images/Image6.png)

#### 2332 (with pin 20 as "active low")
- Switch jumper JP4: 1) Cut one side, 2) solder the other
- Connect JP8 to either 5V or GND, depending on the value you want for address line A12 (starting from A0).
- Cut jumper JP6

#### 2332 (with pin 20 as "active high")
- Install U3 (74LS04)
- Switch jumper JP7: 1) Cut one side, 2) solder the other

#### 2332 (with pin 21 as "active low")
- This is the default. Nothing else to do.

#### 2332 (with pin 21 as "active high")
- Install U3 (74LS04)
- Switch jumper JP5: 1) Cut one side, 2) solder the other

#### 2364 (with pin 20 as "active low")

This is the default configuration. No additional steps are required.

#### 2364 (with pin 20 as "active high")
- Install U3 (74LS04)
- Switch jumper JP7: 1) Cut one side, 2) solder the other

### Q&A

#### Why is the configuration active low?

Some ROMs, especially EEPROMs, have an active-low WRITE pin that needs to be HIGH (or `1`) during normal (read) use. To prevent accidentally putting ROMs into the incorrect mode (write mode instead of read mode), all additional pins are pulled high by default through pull-up resistors.

#### Why are address lines from right to left?

Having them in this orientation was the simplest solution without adding complexity to the design. Additionally, the addressing depends on the type of configuration you use. Binary numbers are typically written from right to left (as implemented), which works best for jumpers, for example. However, DIP switches use labels from left to right.

Overall, one direction had to be chosen, and I opted for the simplest. This can be adjusted by flipping the address bits. ROMs with this fix are already marked with an "f".

### Bill of Materials (BOM)

Below is a list of materials needed to assemble a complete system. Please note that the links and prices (scroll to the right to see them; as of August 22nd, 2024) will not be updated in the future and should only be used as a reference for locating the correct items.

**NOTE**: Links and alternatives are provided to assist you in finding the necessary components. I cannot guarantee the complete accuracy or reliability of all these links and alternatives. Please verify the information for yourself.

| PCB REFERENCE | QTY | VALUE       | COMMENT                                                                                                                                                                                                                          | EACH | TOTAL | SOURCE LINK                                                                               |
| ------------- | --- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- | ----- | ----------------------------------------------------------------------------------------- |
| RN1           | 1   | 4.7k Ohm    | 3 resistor network with 4-pins, bussed resistors                                                                                                                                                                                 | 0.35  | 0.35   | [Mouser](https://www.mouser.com/ProductDetail/652-4604X-1LF-4.7K)                         |
| U1            | 2   |             | Source Link is for a rather expensive version of a machined straight male pin header with 40-pins which can be broken into smaller pieces to server for both. There are cheaper ones, but the link is used for future reference. | 1.0  | 1.0   | [Mouser](https://www.amazon.com/ZYAMY-2-54mm-Breakable-Straight-Connector/dp/B0778KCHHR/) |
| U2            | 1   | 2x64-2x512  | Examples are 23128, 23256, 2764, 27128, 27256, 27512, 2864, 28256 and all other variations such as 27C256 or AT28C64B                                                                                                            | 5.5  | 5.5   | [Mouser](https://www.mouser.com/ProductDetail/556-AT28C64B15PU)                           |
| U3            | 1   | 74LS04  | Optional. Needed for inverting chip select pins. | 0.68  | 0.68   | [Mouser](https://www.mouser.com/ProductDetail/595-SN74LS04D)                           |
| J1            | 1   | -           | Optional. Could be used for right-angle jumpers or attaching ribbon cable to move switch towards more accessible place.                                                                                                          | 1.02 | 1.02  | [Mouser](https://www.mouser.com/ProductDetail/649-1012938294001BLF)                       |
| J2            | 1   | -           | Optional. Adding the ability to switch character sets.                                                                                                                                                                           | 0.27 | 0.27  | [Mouser](https://www.mouser.com/ProductDetail/571-1033222)                                |
|               | 1   | Low-profile | Optional. Adding the ability to switch character sets.                                                                                                                                                                           | 0.67 | 0.67  | [Mouser](https://www.mouser.com/ProductDetail/774-2105MS)                                 |

### RetroStack Libraries

To work with this KiCAD project, you'll need the RetroStack libraries for KiCAD. Please [follow this link](https://www.github.com/RetroStack/KiCAD-Libraries) to access and install these libraries.

## Support this Project

RetroStack is passionate about exploring and preserving the legacy of older computer systems. My work involves creating detailed documentation and videos to share the knowledge. I am also dedicated to reviving these classic systems by reimplementing them and offering replacement parts at no cost. If you're keen on supporting this unique project, I invite you to visit my [Patreon page](https://www.patreon.com/RetroStack). Your support would be immensely valuable and greatly appreciated!

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
