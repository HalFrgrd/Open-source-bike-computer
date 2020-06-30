# Open source-bike-computer
 Designs for an open source bike computer.



## BOM

<!-- ![t-call 1.3 dimensions](tcall_dimensions.png) -->
<!-- |---|---|---|---|---| -->
<!-- |**Preassembled** T-Call v1.3 TTGO ESP32 (no GPS)   | 29 x 7 x 8mm   | $16  | No  |   | -->


||**Item**   | **Dimensions**   | **Cost**  | **Using**  |   |
|---|---|---|---|---|---|
|**Display**|
|| |    | $13   | Yes  |   |
|**Battery and charging**|
||3.7v Lithium Polymer 3200mAh   | 50 x 75 x 7mm  | $8.50  | Yes  |   |
||Receiver pad | 0.5mm thick  | $3  | Yes  |   |
||Charging base  |  | $4  | Yes  |   |
| **Storage** |
||16gb micro SD card   |   | $5  | Yes   |   |
|**Microcontroller and modules** |
||  ESP32 with LiPo charging  |   | $5  | Yes  |   |
|| nrf52840| |$5| Yes||
||  GPS module   |   | $5  | Yes  |   |
||  SIM800L module   |   | $4  | Yes  |   |
|| Micro SD card module  |   | $1  | Yes  |   |
|**Case**|
|| Glass screen protector | | $2 | Yes | |
|| 3D printed enclosure | |  | Yes | |
|| Glue | |  | Yes | |
|| 4 mounting screws | |  | Yes | |
|| 4 threaded heat inserts | |  | Yes | |
|| Rubber o-ring cabling | |  | Yes | |
| **Total** | | | | |

### Actually buying:

[LS027B7DH01](https://www.aliexpress.com/item/33020027250.html?spm=a2g0o.productlist.0.0.36ee3a15mb1GMf&algo_pvid=aad3c1d1-297e-4d29-b040-a34f9ef8f99c&algo_expid=aad3c1d1-297e-4d29-b040-a34f9ef8f99c-1&btsid=0b0a119a15935113972186751eb958&ws_ab_test=searchweb0_0,searchweb201602_,searchweb201603_)
The A indicates maximum of two bright pixels. 
Need an FPC 10 pin connector

## Design

3D printed

The buttons are capacitive pads. 
These pads will be a separate PCB that you can glue onto the 3D printed case.
This will be a water proof seal.
Will the capacitive pads be sensitive to rain?

Maximum target dimensions: 55 wide, 80 long, 20 high 

Need the on off control and charging port to be water proof.

### Capacitive buttons:
ESP32 has 10 capacitive-sensing GPIOs. 
So you don't need to include any extra components to use capacitive buttons
The nrf52 series also don't require any external componenents.

The capacitive pads could perhaps also go under the screen protector.
I'm guessing a screen protector wouldn't reduce the touch sensitivity that much.
This would serve as protection for the capacitive pads.

It is important to reduce the parasitic capacitance and increase the touch capacitance.
How to optimize: reduce trace length by optimizing PCB layout; reduce thickness of the overlay; enlarge electrode's area. 
Could have surface mount pins to reach PCB below.

https://github.com/espressif/esp-iot-solution/blob/master/documents/touch_pad_solution/touch_sensor_design_en.md

https://www.embedded.com/making-capacitive-touch-sensors-water-tolerant/

https://devzone.nordicsemi.com/nordic/short-range-guides/b/design-examples/posts/capacitive-touch-on-the-nrf52-series
### Firmware
https://www.youtube.com/watch?v=lQ157ftTnSs

Google maps platform has a $200 free monthly usage. Could use their route planning.

### Display
[2.42" OLED](https://www.aliexpress.com/item/32950562791.html?spm=a2g0o.productlist.0.0.4f122c2fbCw4XX&algo_pvid=e3eca0d5-b70e-4a4d-96aa-446986a5b739&algo_expid=e3eca0d5-b70e-4a4d-96aa-446986a5b739-2&btsid=0b0a050115931950007767265e4fd4&ws_ab_test=searchweb0_0,searchweb201602_,searchweb201603_)
Not the best choice since they compete with sunlight.

Reflective LCD

https://www.buydisplay.com/blog/what-are-the-main-differences-between-LCD-and-OLED.html

https://www.buydisplay.com/3-4-inch-graphic-touchscreen-lcd-cog-module-240x160-single-sided-fpc
https://www.buydisplay.com/3-inch-touch-240x120-graphic-displays-lcd-serial-interface-black-on-white

https://forum.arduino.cc/index.php?topic=188040.0
https://forum.arduino.cc/index.php?topic=488097.0
https://forum.arduino.cc/index.php?topic=554754.0

Vincent's stravaV10 uses Memory LCD LS027B7DH01
https://makerdyne.com/2015/02/08/large-memory-lcd-breakout-board-details/
https://makerdyne.files.wordpress.com/2015/12/MemoryLCD_Breakout_Board_Schematic.pdf

### Wireless charging
This both for convenience and keeping the enclosure waterproof. 
Quite cheap for a whole setup. The pad inside of the computer can be very slim.


### Contactless payment
https://www.instructables.com/id/RFID-NFC-Tap-and-Go-Ring-for-Credit-Card-Payment/

Could just have a thin slot for a pay as you go card (Revolut or Monzo).Could have SMS notifications so that the bike computer knows when you have paid. 
Set up that sim with that bank card.
Could acetone the bank card to make it slimmer.

### SIM
https://lastminuteengineers.com/sim800l-gsm-module-arduino-tutorial/
I hope to be able to use the microphone pins to play pre-recorded messages.

### PCB design

Pin choice: It seems like the nrf52840 are pretty multi-purpose. For high-frequency stuff, try and avoid pins close to the antenna to avoid interference.
https://devzone.nordicsemi.com/f/nordic-q-a/52857/recommended-pin-usage

P0.0 = 0, P0.1 = 1 .... P0.31 = 31 P1.0 = 32, P1.1 = 33. 

Sharp memory schematics:
https://makerdyne.files.wordpress.com/2015/12/MemoryLCD_Breakout_Board_Schematic.pdf

One set of SPI pins per peripheral: they might work at different speeds. And I think the asynchronous aspect would mean the LCD could be prioritized.

https://github.com/DF4IAH/HFT-Core-Module

Antenna:
SIM868 is L1 band.
Glonass L1: about 1602 MHz
GPS L1: 1575.42 MHz
Beidou: 1575.42 MHz (Possibly lower: 1561.098MHz?)

https://www.antenova.com/integration-hub/antenna-selection-tool/

Drawing antennas as part of the PCB seem like a bad idea. 
They take a lot of testing.

Mouser sells the SR4L049 (both left and right versions) for about 3 dollars. SR4L034 is very similar.

The M20057 and M20047 modules combine the SAW and antenna. Power consumption is about 2ma,

M20047 cost: 4.50 gbp from mouser and at digikey
B3913 cost: 1.62gbp 
SR4L034 cost: 1.44
LNA?:


I'm pretty sure it needs an LNA. So I'm going with 
https://www.u-blox.com/sites/default/files/NEO-8Q-NEO-M8-FW3_HIM_%28UBX-15029985%29.pdf


[Picking a saw filter from Mouser](https://www.mouser.com/pdfdocs/HowToChoosetheOptimalSAWFilter.pdf)

SAW filter: You want something in the middle of the frequencies, so 1588ish and that has a wide enough bandwidth to capture the signals.
Two come up: B3913 and B3413. The B4310 is used in the HFT-Core-Module.
B4310 is from 2015. The B3913 and B3413 are very similar but the B3413 is newer and has improved electrostatic discharge (ESD) robustness. [Qualcomm RF360 website SAW filters for GNSS](https://rffe.qualcomm.com/product/search/automotive/Filters%20for%20GNSS). B4310 doesn't have Beidou next to it on the website. 
I can't find the B3413 in stock, so I'm using the B3913 in stock at digi key.

#### Questions
- The wireless charging setup.
- Battery level indicator.
- Why polarized capacitor in decoupling?
- RF SYNC
- What about low noise ammplifer LNA?


