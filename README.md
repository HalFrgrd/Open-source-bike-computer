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

The capacitive pads could perhaps also go under the screen protector.
I'm guessing a screen protector wouldn't reduce the touch sensitivity that much.
This would serve as protection for the capacitive pads.

It is important to reduce the parasitic capacitance and increase the touch capacitance.
How to optimize: reduce trace length by optimizing PCB layout; reduce thickness of the overlay; enlarge electrode's area. 
Could have surface mount pins to reach PCB below.

https://github.com/espressif/esp-iot-solution/blob/master/documents/touch_pad_solution/touch_sensor_design_en.md

https://www.embedded.com/making-capacitive-touch-sensors-water-tolerant/

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

### Wireless charging
This both for convenience and keeping the enclosure waterproof. 


### Contactless payment
https://www.instructables.com/id/RFID-NFC-Tap-and-Go-Ring-for-Credit-Card-Payment/