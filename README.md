# ESPHome modbus - heatpump cooper and hunter UNITERM 3

## Description:
This manual describes how to connect the device to Home Assistant via Modbus protocol using ESP and RS485/TTL converter.
In this case it is about connecting a UNITERM 3 8kw heat pump.



## Info:
- use only shielded cable, otherwise the error "Modbus CRC Check Failed!" may appear in the log.
- put a 120 ohm resistor after the last connected device
- modbus datasheet: [Gree Versati III](https://github.com/peca2345/ESPHome-modbus-heatpump-Gree-Versati-III/blob/main/modbus-versati-iii-en.pdf)
- you have to find out what the heatpump address is - default is 0x1
- you also need to find out the serial port speed - default 9600
- in ESPHome use the sensor class only for addresses that are read-only
- for addresses that are read/write use the "number" class (you can then change their values in lovelace)
- for each register you want to have in HA you have to create a separate sensor in ESPHome
- you can write the address to the sensor in decimal or hex

## Components:
- ESP8266 / ESP32
- RS485/TTL converter: [SHOP](https://www.laskakit.cz/prevodnik-ttl-na-rs-485--max485/) 

## Schematic ESP32:
![Schema](https://github.com/peca2345/ESPHome-modbus-heatpump-Gree-Versati-III/blob/main/IMG/schematic2.png?raw=true)

## Schematic ESP8266 - Wemos D1 mini:
![Schema](https://github.com/peca2345/ESPHome-modbus-heatpump-Gree-Versati-III/blob/main/IMG/schematic_wemos.png?raw=true)


## Lovelace:
![lovelace](https://github.com/peca2345/ESPHome-modbus-heatpump-Gree-Versati-III/blob/main/IMG/lovelace3.png?raw=true)


## ESPHome code:
Practical tips
You can use the "Heat Pump Error" sensor in HA directly as a trigger for a notification on your phone:
yaml# In HA automation (NOT in this ESPHome config!)
trigger:
  - platform: state
    entity_id: binary_sensor.unitherm3_heat_pump_error
    to: "on"

```    
