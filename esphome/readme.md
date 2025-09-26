# ESPHome Software

This software requires [ESPHome](https://esphome.io/) to be on the ESP32 before it can be used.

Once ESPHome is installed, the [device.yaml](device.yaml) file can be pasted into the device configuration. Some secrets need to be added to ESPHome, or else edit the yaml appropriately.

The code has a configurable section:

```
  name: "ac-infinity-fan-1"
  friendly_name: "ac-infinity-fan-1"
  ap_ssid: "ha-ac-infinity-fan-1"
  ap_password: "ha-ac-infinity"
  ha_api_encryption_key: !secret ha_api_encryption
  esphome_ota_password: !secret esphome_ota_password
  wifi_connect_ssid: !secret wifi_ssid
  wifi_connect_password: !secret wifi_password
  boost_minutes: "30"
  boost_button_mac_address: "00:11:22:33:44:55"
  calibration_mode: "false"
```

| Variable                 | Comments                                                                                                   |
| ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| name                     | The ESPHome/HA name for the device                                                                         |
| friendly_name            | The longer name used to describe the device in the UI                                                      |
| ap_ssid                  | The network name (SSID) to create if wifi cannot be found during boot up                                   |
| ap_password              | The network password of the mini access point created if wifi not found during boot up                     |
| ha_api_encryption_key    | The Home Assistant API encryption key _where to get this?_                                                 |
| esphome_ota_password     | The password used by ESPHome when making Over The Air (OTA) wireless connections                           |
| wifi_connect_ssid        | The network name (SSID) of the wifi network to connect to on boot up                                       |
| wifi_connect_password    | The network password of the wifi used to connect to on boot up                                             |
| boost_minutes            | The number of minutes to run the fan during Boost Mode (specify as a string with quotes around the number) |
| boost_button_mac_address | A MAC address to listen for, if found, activate Boost Mode                                                 |
| calibration_mode         | Boolean to enable calibration mode (see below)                                                             |

## Calibration

The project uses whole numbers from 0-10 to denote the speed of the fan (in the same way as AC Infinity do in their app and on the controller). To make these match with the AC Infinity scale, we have to calibrate the software to match.

Calibration Mode shows a decimal part of the integer speed number. This is a fraction of the "distance" between the lower and upper thresholds of a given speed number. For example, if the lower threshold was 1000 and the upper was 2000, and the current reading was 1230, then the decimal would be .23.

Working out thresholds requires some experimentation and measurements of the actual values received from the fan and controller. Hopefully the values provided here work in most cases, buf if you find selecting (say) speed 3 in the controller shows speed 4 in the Home Assistant UI, then some calibration may be required.
