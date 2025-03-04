# Holybro Pixhawk 6X Wiring Quick Start

:::warning
PX4 does not manufacture this (or any) autopilot.
Contact the [manufacturer](https://shop.holybro.com/) for hardware support or compliance issues.
:::

This quick start guide shows how to power the [Pixhawk 6X<sup>&reg;</sup>](../flight_controller/pixhawk6x.md) flight controller and connect its most important peripherals.

## Kit Contents

### Pixhawk 6X Standard Set

![Pixhawk 6x standard set](../../assets/flight_controller/pixhawk6x/pixhawk6x_standard_set.jpg)

### Pixhawk 6X Mini Set

![Pixhawk 6x mini standard set](../../assets/flight_controller/pixhawk6x/pixhawk6x_mini_set.jpg)


## Wiring Chart Overview

The image below is sample wiring diagram that shows how to connect the most important sensors and peripherals.

![Pixhawk 6x Wiring Overview](../../assets/flight_controller/pixhawk6x/pixhawk6x_wiring_diagram.png)

:::tip
More information about available ports can be found here: [Pixhawk 6X > Connections](../flight_controller/pixhawk6x.md#connections).
:::

## Mount and Orient Controller

*Pixhawk 6X* can be mounted on the frame using double side tape included in the kit.
It should be positioned as close to your vehicle’s center of gravity as possible, oriented top-side up with the arrow pointing towards the front of the vehicle.

<img src="../../assets/flight_controller/pixhawk6x/pixhawk6x_vehicle_front1.jpg" width="400px" title="Pixhawk6x" />

:::note
If the controller cannot be mounted in the recommended/default orientation (e.g. due to space constraints) you will need to configure the autopilot software with the orientation that you actually used: [Flight Controller Orientation](../config/flight_controller_orientation.md).
:::

## GPS + Compass + Buzzer + Safety Switch + LED

The _Pixhawk6X Standard Set_ & _Pixhawk6X Mini Set_ can be purchased with M8N or M9N GPS (10-pin connector) that should be connected to the **GPS1** port.
These GNSS modules have an integrated compass, safety switch, buzzer and LED.

A secondary [M8N or M9N GPS](https://shop.holybro.com/c/gps-systems_0428) (6-pin connector) can be purchased separately and connected to the **GPS2** port.

The GPS/Compass should be [mounted on the frame](../assembly/mount_gps_compass.md) as far away from other electronics as possible, with the direction marker towards the front of the vehicle (separating the compass from other electronics will reduce interference).

<img src="../../assets/flight_controller/pixhawk5x/pixhawk5x_gps_front.jpg" width="200px" title="Pixhawk5x standard set" />


:::note
The GPS module's integrated safety switch is enabled *by default* (when enabled, PX4 will not let you arm the vehicle).
To disable the safety press and hold the safety switch for 1 second.
You can press the safety switch again to enable safety and disarm the vehicle (this can be useful if, for whatever reason, you are unable to disarm the vehicle from your remote control or ground station).
:::


## Power

Connect the output of the *PM02D Power Module* (PM board) that comes with the Standard Set to one of the **POWER** port of *Pixhawk 6X* using the 6-wire cable.
The PM02D and Power ports on the Pixhawk 6X uses the 6 circuit [2.00mm Pitch CLIK-Mate Wire-to-Board PCB Receptacle](https://www.molex.com/molex/products/part-detail/pcb_receptacles/5024430670) & [Housing](https://www.molex.com/molex/products/part-detail/crimp_housings/5024390600).

The PM02D Power Module supports **2~6S** battery, the board input should be connected to your LiPo battery. Note that the PM board does not supply power to the + and - pins of **FMU PWM OUT** and **I/O PWM OUT**.

If using a plane or rover, the **FMU PWM-OUT** will need to be separately powered in order to drive servos for rudders, elevons etc. This can be done by connecting the 8 pin power (+) rail of the **FMU PWM-OUT** to a voltage regulator (for example, a BEC equipped ESC or a standalone 5V BEC or a 2S LiPo battery).

:::note
The power rail voltage must be appropriate for the servo being used!
:::

PIN & Connector | Function
--- | ---
I/O PWM Out | Connect Motor Signal and GND wires here.
FMU PWM Out | Connect Servo Signal, positive, and GND wires here.


:::note
**MAIN** outputs in PX4 firmware map to **I/O PWM OUT** port of *Pixhawk 6X* whereas **AUX outputs** map to **FMU PWM OUT** of *Pixhawk 6X*.
For example, **MAIN1** maps to IO_CH1 pin of **I/O PWM OUT** and **AUX1** maps to FMU_CH1 pin of **FMU PWM OUT**.
:::


The pinout of *Pixhawk 6X*’s power ports is shown below. The power ports takes in I2C digital signal from the PM02D power module for voltage and current data. The VCC lines have to offer at least 3A continuous and should default to 5.2V. A lower voltage of 5V is still acceptable, but discouraged.

Pin | Signal | Volt
--- | --- | ---
1(red) | VCC | +5V
2(black) | VCC | +5V
3(black) | SCL | +3.3V
4(black) | SDA | +3.3V
5(black) | GND | GND
6(black) | GND | GND

## Radio Control

A remote control (RC) radio system is required if you want to *manually* control your vehicle (PX4 does not require a radio system for autonomous flight modes).

You will need to [select a compatible transmitter/receiver](../getting_started/rc_transmitter_receiver.md) and then *bind* them so that they communicate (read the instructions that come with your specific transmitter/receiver).

- Spektrum/DSM receivers connect to the **DSM/SBUS RC** input.
- PPM or SBUS receivers connect to the **RC IN** input port.

PPM and PWM receivers that have an *individual wire for each channel* must connect to the **RC IN** port *via a PPM encoder* [like this one](http://www.getfpv.com/radios/radio-accessories/holybro-ppm-encoder-module.html) (PPM-Sum receivers use a single signal wire for all channels).

For more information about selecting a radio system, receiver compatibility, and binding your transmitter/receiver pair, see: [Remote Control Transmitters & Receivers](../getting_started/rc_transmitter_receiver.md).


## Telemetry Radios (Optional)

[Telemetry radios](../telemetry/README.md) may be used to communicate and control a vehicle in flight from a ground station (for example, you can direct the UAV to a particular position, or upload a new mission).

The vehicle-based radio should be connected to the **TELEM1** port as shown below (if connected to this port, no further configuration is required).
The other radio is connected to your ground station computer or mobile device (usually by USB).

Radios are also available for purchase on [Holybro's website](http://www.holybro.com/product-category/radio/) .

## SD Card (Optional)

SD cards are highly recommended as they are needed to [log and analyse flight details](../getting_started/flight_reporting.md), to run missions, and to use UAVCAN-bus hardware.
Insert the card (included in Pixhawk 6X) into *Pixhawk 6X* as shown below.

<img src="../../assets/flight_controller/pixhawk5x/pixhawk5x_sd_slot.jpg" width="420px" title="Pixhawk5x standard set" />

:::tip
For more information see [Basic Concepts > SD Cards (Removable Memory)](../getting_started/px4_basic_concepts.md#sd-cards-removable-memory).
:::

## Motors

Motors/servos are connected to the **I/O PWM OUT** (**MAIN**) and **FMU PWM OUT** (**AUX**) ports in the order specified for your vehicle in the [Airframe Reference](../airframes/airframe_reference.md).

:::note
This reference lists the output port to motor/servo mapping for all supported air and ground frames (if your frame is not listed in the reference then use a "generic" airframe of the correct type).
:::

:::warning
The mapping is not consistent across frames (e.g. you can't rely on the throttle being on the same output for all plane frames). Make sure to use the correct mapping for your vehicle.
:::

## Other Peripherals

The wiring and configuration of optional/less common components is covered within the topics for individual [peripherals](../peripherals/README.md).

## Pinouts

* [Holybro Pixhawk Baseboard Pinout](https://docs.holybro.com/autopilot/pixhawk-6x/pixhawk-baseboard-pinout)
* [Holybro Pixhawk Mini-Baseboard Pinout](https://docs.holybro.com/autopilot/pixhawk-6x/pixhawk-mini-baseboard-pinout)

## Configuration

General configuration information is covered in: [Autopilot Configuration](../config/README.md).

QuadPlane specific configuration is covered here: [QuadPlane VTOL Configuration](../config_vtol/vtol_quad_configuration.md)

<!-- Nice to have detailed wiring infographic and instructions for different vehicle types. -->

## Further information

- [Holybro Docs](https://docs.holybro.com/) (Holybro)
- [Pixhawk 6X](../flight_controller/pixhawk6x.md) (PX4 Doc Overview page)
- [PM02D Power Module](../power_module/holybro_pm02d.md)
- [PM03D Power Module](../power_module/holybro_pm03d.md)
- [Pixhawk Autopilot FMUv6X Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-012%20Pixhawk%20Autopilot%20v6X%20Standard.pdf).
- [Pixhawk Autopilot Bus Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf).
- [Pixhawk Connector Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf).
