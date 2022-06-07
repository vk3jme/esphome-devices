---
title: Verve Design Hana 24W CCT Ceiling Light (ACL03HA)
date-published: 2022-06-07
type: light
standard: au
---

## GPIO Pinout

| Pin    | Function                  |
| ------ | ------------------------- |
| GPIO14 | PWM `(brightness)` |
| GPIO12 | PWM `(color_temp)` |

## Basic Configuration

```yaml
# Basic Config
substitutions:
  device_name: "ceiling-light"
  friendly_name: "Ceiling Light"
  device_description: "Verve Design Hana 24W CCT Ceiling Light (ACL03HA)"

esphome:
  name: ${device_name}
  comment: ${device_description}
  platform: ESP8266
  board: esp8285

wifi:
  ssid: "ssid"
  password: "password"

logger:

api:
  password: "api_password"

ota:
  password: "ota_password"

sensor:
  - platform: uptime
    name: ${name} Uptime

  - platform: wifi_signal
    name: ${name} Signal
    update_interval: 300s

output:
  - platform: esp8266_pwm
    id: dimmer
    pin: GPIO14
  - platform: esp8266_pwm
    id: colour_temp
    pin: GPIO12
    inverted: true


light:
  - platform: color_temperature
    name: ${friendly_name}
    color_temperature: colour_temp
    brightness: dimmer
    cold_white_color_temperature: 6500 K
    warm_white_color_temperature: 3000 K
    restore_mode: ALWAYS_ON
