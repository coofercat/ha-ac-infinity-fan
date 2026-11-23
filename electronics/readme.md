# HA AC Infinity Electronics

The electronics for the HA AC Infinity project require a few components:

- An ESP32-32S WROOM board (eg. https://www.amazon.co.uk/dp/B0DQ51N5B1 or https://www.aliexpress.us/item/3256806910572056.html). Ensure it's the 38-pin version.
- A USB-C socket (eg. https://www.amazon.co.uk/dp/B0D59Y34ZF or https://www.aliexpress.us/item/3256809620386955.html)
- A male-to-male UIS cable (eg. https://www.amazon.co.uk/dp/B0BRNVBJRN or https://www.amazon.com/dp/B0DPJDC46R)
  - See [note below](#connecting-the-usb-connectors) on UIS v2 cable colors
- Two 3D printed parts to make the box (although other boxes are also possible)
- Four M3 x 5mm and 4 M3 x 12mm self-tapping screws to hold it together
- Some short lengths of general purpose multi-strand hookup wire (ideally in a few different colours)

There is also a whole [Bill Of Materials](https://html-preview.github.io/?url=https://github.com/coofercat/ha-ac-infinity-fan/blob/main/electronics/ac-infinity-esphome_bom.html) (BOM) for the electronic circuit. The circuit uses mostly generic, easy to source through-hole components. It's relatively easy to solder together. The transistors I used are 2N3904, and I used a buck module (https://www.amazon.co.uk/dp/B081JMJZG6) instead of a regular 7805 voltage regulator (if you do use a 7805, you will also need a heatsink). The relay is a generic 5V coil, DPDT (I had some of these already). The BOM lists JP1 and JP2, but these are not needed - they're just holes for attaching wires.

I also had PCBs made, which is optional but recommended (you get a lot of electrical noise in this circuit, so trying to make it work on a breadboard or stripboard is likely to be difficult). There is a [Fritzing file](ac-infinity-esphome.fzz) and [exported Gerber files](ha-ac-infinity-gerber-export/) available if you want to make a PCB.

If you're starting from scratch, some initial suggestions on components - double check you select the right types on each page before ordering:
- [Tantalum capacitors](https://www.aliexpress.us/item/3256805727914856.html)
- [5V DPDT relays](https://www.aliexpress.us/item/3256804869398804.html)
- [5V step-down buck modules](https://www.aliexpress.us/item/3256806393040704.html)
- [Assorted transistor kit](https://www.aliexpress.us/item/3256806022216265.html)
- [Assorted resistor kit](https://www.aliexpress.us/item/3256807801500827.html)
- [Assorted diode kit](https://www.aliexpress.us/item/3256808445229474.html)

## Making the Electronics

### Noise and Malfunctions

When I first made this project, everything worked fine on the desk. However, when I put it into service a persistent problem occurred. The problem looks like it's possibly electrical noise on the PWM signal line, although no amount of decoupling and shielding seems to stop it. I tracked the problem down to the male USB plug and wire to the board. The DIY USB connectors I was using appear to be the problem, although I also tried pre-made moulded USB 'pig tails' and they also didn't work (I actually made up 4 of these circuit boards and USB connectors using the DIY connectors - one of them works flawlessly, the others all exhibit the problem). **The only solution I have found that works reliably is to cut up an AC Infinity UIS cable**. Whilst a comparitively expensive option, it does mean you get a nicely moulded USB connector (I also tried using the UIS cable with a DIY USB plug, that also didn't work). If anyone finds a better, reliable, solution, I'd love to hear about it!

The problem manifests itself as the fan resetting itself every few seconds. That is, when the controller requests (say) speed 5, the fan speeds up, but then resets (making a slight clicking noise), slows down and then speeds up again. The controller doesn't show anything, but the mobile app shows the actual speed fluctuating. I looked at the PWM signal on an oscilloscope, I can't really see any problem with it, but during a reset it stops "pwming" for a moment, which is when the fan resets. It's unclear why the controller does this, or how it's aware of a problem as the whole system works without the Tach signal, so there's no "input" to the controller.

### USB Connectors

AC Infinity misuse USB connectors for their proprietary connections. Their system is absolutely not compatible with any genuine USB devices, and will likely catastrophically damage them if you are foolish enough to connect them to it.

Contrary to just about all the information elsewhere in the Internet, the AC Infinity UIS protocol is a **5** pin protocol (I got desperate and cut up an official cable!). The pin out is:

| Wire Colour | USB Pin   | Purpose     |
| ----------- | --------- | ----------- |
| Red         | VBUS      | +10V power  |
| Yellow      | D+        | Tach Signal |
| White       | D-        | PWM         |
| Black       | GND       | Ground      |
| Green       | CC1 & CC2 | ???         |

The CC1/CC2 (green) connection doesn't appear to be necessary to make this project work. I'd connect it if you have connectors that have it, otherwise don't worry about it too much. It's likely only used in more complex setups, which aren't supported by this project.

Since I'm now using cut-up UIS cables as part of the project, in board revision 3.1 I've changed the colour scheme on the board to match the UIS colours:

| Socket | AC Infinity | Colour Coding |
| ------ | ----------- | ------------- |
| V      | +10V        | Red           |
| D+     | Tach Signal | Yellow        |
| D-     | PWM         | White         |
| G      | Ground      | Black         |

For the plug, cut about 15-20cm off the end of a UIS cable. Strip maybe 1-2cm of the outer insulation and then strip a couple of millimetres off each of the four signal wires inside. You don't need to do anything with the green wire.

For the socket, you need four 50mm lengths of multi-strand wire. Strip one end to a couple of millimeters, insert into the holes on the socket and solder into place. Again, strip the other end to maybe 5mm, but don't tin them.

USB socket wiring - note the colours here are the old 3.0 colours!

[<img src="2-usb-socket-wiring.jpg" width="300" height="auto">](2-usb-socket-wiring.jpg)

### Making the PCB

The PCB uses through-hole components, which are hopefully easy to fit and solder. Most components lie against the board, although a few resistors are vertical (R7 & R8). Please note that if a 7805 voltage regulator is used (instead of a compatible module) then a heat sink will be required.

See the [Bill Of Materials](https://html-preview.github.io/?url=https://github.com/coofercat/ha-ac-infinity-fan/blob/main/electronics/ac-infinity-esphome_bom.html) for a full list of components required and where to fit them. Note that JP1 and JP2 are not required - instead their holes can be used to connect wires from the USB sockets (see below).

| Step                                                                                       | Step                          |
| ------------------------------------------------------------------------------------------ | ----------------------------- |
| [<img src="3-empty-board.jpg" width="300" height="auto">](3-empty-board.jpg)               | Start with an empty board...  |
| [<img src="4-passive-components.jpg" width="300" height="auto">](4-passive-components.jpg) | Add the passive components... |
| [<img src="5-active-components.jpg" width="300" height="auto">](5-active-components.jpg)   | Add the active components...  |

### Connecting the USB Connectors

JP1 (left) connects to the controller. Use the cut up UIS cable's plug for this connection. If using a UIS v2 cable, the white (PWM) and yellow (tach) wires may be reversed — if the controller speed reads incorrectly, try swapping them on JP1. There's a low risk of damage if these two are incorrectly wired.

JP2 (right) connects to the fan via a USB socket and a male-to-male UIS cable. Four short wires from the socket to the board is all that's needed. 

Note the colour coding of the holes on the PCB, from the top of the board to the bottom:

| JP1    | JP2    |
| ------ | ------ |
| Red    | Black  |
| Yellow | White  |
| White  | Yellow |
| Black  | Red    |

Once assembled it should look like this:

[<img src="6-fully-assembled.jpg" width="300" height="auto">](6-fully-assembled.jpg)

### Fitting the board into the box

The board should screw into the box using four M3 5mm self-tapping screws. The 4 core cable should fit into the cable gland, and be held into place by a strain-relief grip. The USB socket should fit into the slot on the side of the box.

[<img src="7-in-box.jpg" width="300" height="auto">](7-in-box.jpg)
