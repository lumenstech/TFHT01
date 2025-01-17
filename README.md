

# TFHT01 - UAV Humidity and Temperature Sensor

<a href="https://certification.oshwa.org/cz000010.html" title="Open Source Hardware Association Certificate"><img align="right" src="https://github.com/ThunderFly-aerospace/TFHT01/assets/5196729/b0df7c2c-4afa-4363-931a-d4acda329d87" width="15%" alt="Open Source Hardware Association Certificate"></a>
[![Kicad](https://github.com/ThunderFly-aerospace/TFHT01/actions/workflows/kicad_outputs.yml/badge.svg?branch=TFHT01B)](https://github.com/ThunderFly-aerospace/TFHT01/actions/workflows/kicad_outputs.yml)

The TFHT01 hygrometer sensor offers flexible integration options. It can be directly connected to a Pixhawk autopilot with PX4 firmware, or it can be used as a sensor for the [TF-ATMON monitoring system](https://www.thunderfly.cz/tf-atmon.html).

Sensors mounted on UAVs can be used for a variety of purposes. TFHT01 can measure air temperature and humidity, which can be used for meteorological purposes to estimate whether icing may form on aerodynamic surfaces. It could also be used to determine if the flight is conducted within the operating range of the drone. Another use can be to measure the temperature of selected UAV components, for example, the temperature of batteries, ESC, motor, or some bearings. 

![TFHT01A top view](/doc/img/TFHT01B_boxes.jpg)

## Where to get it?

The TFHT01 is commercially available from [ThunderFly s.r.o.](https://www.thunderfly.cz/). For a commercial quotation or support, contact us by email at sale@thunderfly.cz or shop at [Tindie store](https://www.tindie.com/products/thunderfly/tfht01-aerial-hygrometer-and-thermometer/).


## Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Sensing element | [SHT35](https://sensirion.com/media/documents/213E6A3B/63A5A569/Datasheet_SHT3x_DIS.pdf) | Other possible sensors are SHT30 or SHT31 |
| Typical accuracy | 1.5 %RH and 0.1 °C | |
| Repeatability | 0.15 %RH , 0.08 °C | The stated repeatability is 3 times the standard deviation (3σ) of multiple consecutive measurements at constant ambient conditions. |
| Operating temperature range| 0 °C - +65 °C | Sensor physically measures in range -40°C to +120°C with reduced accuracy |
| Operating humidity range| 0-100 % | At humidity above 80% the performance of the sensor could be degraded in case of prolonged periods |
| I2C connector | 4-pin JST-GH | The second connector could be installed on the opposite side |
| I2C address | 0x44 default | By switching of JP1 is possible change address to 0x45 |
| Storage temperature range| -20 °C - +40 °C |  |
| Operational input voltage | 3.6 - 5.4V | Overvoltage internally protected by zener diode |
| Mass | 2 g | PCB without cabling |
| Dimensions | 30 x 15 x 6.5 mm |  PCB |
| Weather resistance | IP40 | External connectors fully occupied. The sensor itself could be protected by IP67 according the [sensirion datasheet](https://sensirion.com/media/documents/9D103E42/61641F0F/Sensirion_Humidity_Sensors_SHT3x_Datasheet_Filter_Membrane.pdf) |


## Applications

### Atmospheric sounding

The TFHT01 sensor could be used for [direct atmospheric sounding](https://en.wikipedia.org/wiki/Atmospheric_sounding). Here is an example of measured data taken by [TF-G2 autogyro](https://www.thunderfly.cz/tf-g2.html).

![TFHT01A atmospheric profiling](/doc/img/TFHT_vertical_profile_measurement.png)

## Design

![TFHT01A top view](/doc/img/tfht01B_small.png)

### Schematics

[![Schematics](/doc/gen/TFHT01-schematic.svg)](/doc/gen/TFHT01-schematic.pdf)

## Usage in PX4 autopilot firmware

The PX4 autopilot firmware supports the sensor. Multiple sensors can be connected to one autopilot. The measured data are immediately sent to the ground station and they are also logged in the onboard ulog file. Sensor support can be enabled by setting the [SENS_EN_SHT3X](http://docs.px4.io/master/en/advanced_config/parameter_reference.html#SENS_EN_SHT3X) parameter to 1.


### Driver Commands Examples

CLI usage example:

    sht3x start -X

Start the sensor driver on the external bus

    sht3x status

Print driver status

    sht3x values

Print the last measured values

    sht3x reset

Reinitialize senzor, reset flags

### PX4 Driver Usage

```
sht3x <command> [arguments...]
 Commands:
   start
     [-I]        Internal I2C bus(es)
     [-X]        External I2C bus(es)
     [-b <val>]  board-specific bus (default=all) (external SPI: n-th bus
                 (default=1))
     [-f <val>]  bus frequency in kHz
     [-q]        quiet startup (no message if no device found)
     [-a <val>]  I2C address
                 default: 68
     [-k]        If initialization (probing) fails, keep retrying periodically

   stop

   status        print status info

   values        Print actual data

   reset         Reinitialize sensor
```

## Usage in Ardupilot firmware

In the Ardupilot firmware, the corresponding sht3x driver for TFHT01 is currently missing. The contributions are welcomed. 

## Resources

  * [ThunderFly TFHT01 documentation page](https://docs.thunderfly.cz/avionics/TFHT01/)
  * [Store](https://www.tindie.com/products/26354/)
  * [Contact details](https://www.thunderfly.cz/contact-us.html)
