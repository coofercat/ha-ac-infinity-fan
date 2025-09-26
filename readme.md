# HA AC Infinity Fan Controller

The AC Infinity Cloudline growing fans (such as the S4, S5, S6) are fantastic smart fans. They're made for growing rooms and the like, but also have a use in domestic bathrooms. They have temperature and humidistat probes and can be programmed to speed up the fan as humidity increases. This makes them ideal to suck out the steam after a shower.

Side note: in the UK, all houses have to have an Energy Performance Certificate (EPC). EPCs now take into account things like ventilation, energy efficiency etc. Smart fans can help improve your EPC because you can show continuous forced ventilation, and variable speed extraction of humidity (which is better than running on
a timer, or even at full speed to a fixed humidity level).

Whilst AC Infinity fans can connect to Wifi or Bluetooth, sadly, they do not (yet) come with any publicly accessible API. As such, the likes of Home Assistant can't directly interface with them. Hopefully one day AC Infinity will see the value in such things, but until then, we have to use different methods to hook these fans into our home automation.

## About This Project

This project aims to provide Home Assistant integration to AC Infinity Cloudline fans, but also aims to leave all the original manufacturer functionality in place. This allows for flexibility and creativity in Home Assistant, but leaves the fans "as intended" and usable by any future owners.

In terms of implementation, this project puts some electronics "between" the AC Infinity controller display and the fan itself. It's entirely powered by the fan, and unless Home Assistant instructs it otherwise, it just passes AC Infinity signals from the controller to the fan completely unaltered.

Home Assistant is able to read the speed requested by the AC Infinity controller, the actual speed of the fan itself (via its tach signal), and is able to "switch out" the controller and provide signals to drive the fan itself if needed. There is no way to read the temperature or humidistat sensors on the AC Infinity controller though (if that's required, other projects may be more to your liking than this one).

Since this project was for use in bathrooms, we also provides an optional Boost Button. That is, a button which can be used to request 30 minutes of maximum speed fan extraction, perhaps to remove smells. The button is completely optional and does not require Home Assistant to be running or available to make it work.

The whole thing is based around an ESP32-32S WROOM (CP2012) and ESPHome. A few pins of the ESP are used as inputs and outputs, the bluetooth is used as a BLE receiver (for the Boost Button), the Wifi connects it to Home Assistant.

## Documentation

- [About the Electronics](electronics/readme.md)
  - [Electronics 3D Printed box](electronics/3d-printer/readme.md)
- [About the Boost Button](boost-button/readme.md)
  - [Boost Button 3d Printed box](boot-button/3d-printer/readme.md)
- [About the ESPHomeSoftware](esphome/readme.md)
- [FAQ](faq.md)
- [License](LICENSE.md)

## Authors Note

This project is Creative Commons licensed, so you're pretty much free to do what you like with it, so long as you credit the original author. If you do make it, we'd love to hear about what you're doing with it though, so please do get in contact.
