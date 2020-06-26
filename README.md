# Open source-bike-computer
 Designs for an open source bike computer.



## BOM

<!-- ![t-call 1.3 dimensions](tcall_dimensions.png) -->
<!-- |---|---|---|---|---| -->
<!-- |**Preassembled** T-Call v1.3 TTGO ESP32 (no GPS)   | 29 x 7 x 8mm   | $16  | No  |   | -->


||**Item**   | **Dimensions**   | **Cost**  | **Using**  |   |
|---|---|---|---|---|---|
|**Display**|
||2.42" OLED | 43 x 71mm   | $15   | Yes  |   |
|**Battery**|
||3.7v Lithium Polymer 3200mAh   | 50 x 75 x 7mm  | $8.50  | Yes  |   |
| **Storage** |
||16gb micro SD card   |   | $5  | Yes   |   |
|**Microcontroller and modules** |
||  ESP32 with LiPo charging  |   | $5  | Yes  |   |
||  GPS module   |   | $5  | Yes  |   |
||  SIM800L module   |   | $4  | Yes  |   |
||Micro SD card module  |   | $1  | Yes  |   |
|**Case**|
|| Glass screen protector | | $2 | Yes | |
| **Total** | | | | |

## Design

3D printed

The buttons are capacitive pads. 
These pads will be a separate PCB that you can glue onto the 3D printed case.
This will be a water proof seal.
Will the capacitive pads be sensitive to rain?

Maximum target dimensions: 55 wide, 80 long, 20 high 

### Capacitive buttons:
ESP32 has 10 capacitive-sensing GPIOs. 
So you don't need to include any extra components to use capacitive buttons

The capacitive pads could perhaps also go under the screen protector.
I'm guessing a screen protector wouldn't reduce the touch sensitivity that much.
This would serve as protection for the capacitive pads.

It is important to reduce the parasitic capacitance and increase the touch capacitance.
How to optimize: reduce trace length by optimizing PCB layout; reduce thickness of the overlay; enlarge electrode's area. 


https://github.com/espressif/esp-iot-solution/blob/master/documents/touch_pad_solution/touch_sensor_design_en.md

### Firmware
https://www.youtube.com/watch?v=lQ157ftTnSs

Google maps platform has a $200 free monthly usage. Could use their route planning.