# HA AC Infinity Frequently Asked Questions

## Why have a 'takeover' and 'pass through'? Why not control the fan directly?

The aim of this project was to be as "low impact" as possible, and to let the fans operate as the manufacturer intended _unless_ the user specifically wants something different. If the fans get built into a house, then
this avoids "the house that Jack built" problems, and lets any future owner use the fans as normal if they want to. It also lets the fans operate via the controller (and perhaps the AC Infinity phone app), even if home automation is unavailable.

## Why did you use a relay? Surely $some_other_solution is better?

Originally I tried to get the circuit to work with a a 74HC00, acting as a switch. I had problems with getting the PWM signals from the controller and from the ESP32 to work properly, so changed it to use a relay instead. There are quite probably better solid state solutions available, and I'd be happy to see any working improvements.

## What transistors are needed to make the electronics?

You can use any reasonably fast, low power transistors. I used 2N3904s, but any NPN transistors with a similar sort of capability will do fine.

## Can you/how do you read temperature and humidity from the controller?

This project does not have access to the temperature or humidity (or other readings) the controller has available. Unless AC Infinity make some sort of API, we have to work without.

Other projects completely replace the AC Infinity controller, and so the sensor probe plugs into them instead of the controller. Those projects do have access to the environmental readings, but then become the sole source of control of the fan (which isn't what this project aimed to do).

# What can Home Assistant do to the fan with this project?

HA can read the controller's speed signal and it can read the fan's tach speed signal. Therefore it can determine what the controller has requested, and what the fan is actually doing. Further, it is able to disconnect the controller's speed request signal and insert its own instead, thus it can make the fan run at a different speed than the controller may be set to at the time.

## Can this work with other fans in the AC Infinity range?

I don't know for sure. The CloudLine range all work the same way, so are all compatible. Other lines may also work, but I haven't tested them. I'd welcome any proven information on any of them.

## Can this work with multiple fans connected to the same controller?

Yes, although each set of electronics only works with one fan. Therefore you'd need a set of electronics for each fan you want to control.

## Can I use this project with some other product or different manufacturer?

Probably not. The AC Infinity connections and signals are proprietary and very much not USB standard, so it's unlikely any other manufacturer would happen to have adopted the same specifications. Products other than fans are also unlikely to work with this without modification.

## Can you make parts of this project for me?

Sadly, no. You may be able to find companies that can 3D print things for you, someone like JLCPCB can make the PCB for you and may even assemble the circuit board for you though. At the end of the day, this is a "DIY" project, so you may have to solve some problems yourself.

## What is the Boost Button?

The Boost Button is a physical button which sends a signal to the HA AC Infinity electronics. On receipt, the electronics takes control of the fan, and requests it runs at full speed for 30 minutes. At the end of that time, it goes back to however it was before the button was pushed. None of this needs Home Assistant, so it works 'offline' if necessary. It can be triggered via Home Assistant as well, so if you have another way to "push the button", it's possible to do that too.

## I've heard you should use opto-isolators with AC Infinity fans because of concerns about mains...?

I've heard this too. I'm no expert, but my take on it is that if mains does appear on any of the four power/signal lines, it's going to cause a whole world of problems for the fan and controller, so whatever happens to this additional electronics is really the least of those problems. It would also call into question the general safety and quality of the fan product as a whole, probably making it unsuitable for any domestic use.

## Can I reprogramme the ESP32 while its soldered on the board?

Yes you can. For most updates you can use ESPHome's wireless Over The Air (OTA) feature. If you need to directly connect with a USB cable you can do this, but disconnect the board from the AC Infinity while you do so. You will need to remove the board from the box to get access to the ESP32's USB socket.

## How is this project licensed? Do I need to pay for it or anything else?

The project is Creative Commons licensed, so you can pretty much do what you like with it, so long as you credit the original author. You don't need to pay to use it.

## Do I need to tell you if I've made any of this project?

No, but I'd love to hear from you if you do. It's be great to hear what you're using it for.

## What if my question isn't answered?

Feel free to get in touch (via Github's 'Issues').
