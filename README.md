# esp32-temp-c

[![license](https://img.shields.io/github/license/mashape/apistatus.svg)]()

## Introduction

This is largely based on an [example application](https://github.com/DavidAntliff/esp32-ds18b20-example) for the Maxim Integrated DS18B20 Programmable Resolution 1-Wire Digital Thermometer device.

Ensure that submodules are cloned:

```
$ git clone --recursive https://github.com/jknutson/esp32-temp-c.git
```

Build the application with:

```
$ cd esp32-temp-c
$ idf.py menuconfig    # set your Wifi, MQTT, and 1-Wire GPIO configuration - see below
$ idf.py build
$ idf.py -p (PORT) flash monitor
```

The program should detect your connected devices and periodically obtain temperature readings from them, displaying them
on the console and publishing to an MQTT topic.

## Dependencies

This application makes use of the following components (included as submodules):

 * components/[esp32-owb](https://github.com/DavidAntliff/esp32-owb)
 * components/[esp32-ds18b20](https://github.com/DavidAntliff/esp32-ds18b20)

## Hardware

To run this example, connect one or more DS18B20 devices to a single GPIO on the ESP32. Use the recommended pull-up 
resistor of 4.7 KOhms, connected to the 3.3V supply.

`idf.py menuconfig` can be used to set the 1-Wire GPIO.

If you have several devices and see occasional CRC errors, consider using a 2.2 kOhm pull-up resistor instead. Also 
consider adding decoupling capacitors between the sensor supply voltage and ground, as close to each sensor as possible.

If you wish to enable a second GPIO to control an external strong pull-up circuit for parasitic power mode, ensure 
`CONFIG_ENABLE_STRONG_PULLUP=y` and `CONFIG_STRONG_PULLUP_GPIO` is set appropriately.
 
See documentation for [esp32-ds18b20](https://www.github.com/DavidAntliff/esp32-ds18b20-example#parasitic-power-mode)
for further information about parasitic power mode, including strong pull-up configuration.


## License

The code in this project is licensed under the MIT license - see LICENSE for details.

## Links

 * [DS18B20 Datasheet](http://datasheets.maximintegrated.com/en/ds/DS18B20.pdf)
 * [Espressif IoT Development Framework for ESP32](https://github.com/espressif/esp-idf)

## Acknowledgements

"1-Wire" is a registered trademark of Maxim Integrated.
