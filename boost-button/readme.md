# HA-AC-Infinity Boost Button

[<img src="11-completed-button.jpg" width="300" height="auto" align="right">](11-completed-button.jpg)

The Boost Button is a way to request the fan comes on (at full speed)
for a period of time (currently programmed at 30 minutes). It's a
physical device with a big button on the top which can be put somewhere
in the bathroom, should anyone, er, "make smells" and want to have
some ventilation.

Internally, the button is made of some bought components:

- A so-called "iTag" key finder (BLE beacon), such as these: https://www.amazon.co.uk/dp/B0FH64TKKL
- A 22mm mushroom button, such as these: https://www.amazon.co.uk/dp/B0DB28T1KS
- Two AAA single battery holders, such as these: https://www.amazon.co.uk/dp/B0B9NJ14WL
- Some 3D printed parts to make a sort of "hockey puck" box
- Some small screws to hold things together (eg. 4 off M2.3 x 5-8mm round head, 2 off M2.3 x 5mm countersunk)

There are full [instructions](instructions.md) for how to construct the button.

## About the BLE Beacon

The "ITag" devices are super-cheap (you get four in pack for less than one of the "better" brands).
They're probably not very good at being key finders (mainly because the phone app they use is pretty poor),
but they work really well for this project.

These devices identify as "iTag", manufactured by "Ubiquitous Computing Technology Corporation". My scanner says they use the "Legacy" scanning type, and are LE only. They're connectable, and there are some capabilities once connected. The original phone app is able to make them beep remotely, so there's presumably a capability to do that in there somewhere.

The main feature that they need is that they must BLE beacon as soon as they're powered up. Some
brands do this, some do not (those tend to need you to press the button to start the beaconing
process). The Boostt Button has a single button, which we use to isolate power from the beacon to
specifically stop it beaconing (and to save battery). As such, we really do need it to start
beaconing as soon as we power it up. Some other brands of key finder can have their buttons
permanently pressed to do the same thing - if you can't find the iTag type, then some
experimentation may be needed.

You may want to look into using a phone app BLE scanner. I've been using nRF Connect (by Nordic Semiconductor). It seems to do a good job of finding these sorts of tags and giving out as much information as they have in them.

## About the Box

The box for this is 3D printed. You can of course use a different box, and if you use different
beacons, you're going to have to modify the box at the very least, if not design it differently.
The same is true if you use a different type of button.

In terms of printing, the box needs support to be able to print it. On my BambuLabs A1, with a single
filament, the support was sufficiently easy to remove and left good enough quality inside (all the
outside surfaces print beautifully). If you've got multiple materials and can do fancy support then
you're likely to get better internal quality than I did, but I'm not sure it's all that necessary.

The box is made of two parts which screw together from the bottom. You need to undo four small screws to be able to change the batteries.
