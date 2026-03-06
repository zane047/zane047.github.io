# Component Selection — Team 307

---

## 1. 5 V, 1.5 A Regulator

| Solution | Pros | Cons |
|-----------|------|------|
| **Option 1 — 7805 Linear Regulator (TO-220)** <br>Dropout ≈ 2 V<br>Simple 2-capacitor application<br>Price: ~$1–$2 (qty 1)<br>[Product Page](https://www.digikey.com/en/products/filter/linear-voltage-regulators/699)<br>![LM7805](Thing_1.png) | • Very simple and low-noise output<br>• Easy to source and short lead time<br>• Excellent line/load regulation | • Inefficient from 12 V → 5 V<br>• Needs heatsink above ~300 mA<br>• Dropout ≈ 2 V limits low-Vin |
| **Option 2 — 5 V Buck Module (e.g., MP1584 / LM2596)** <br>High-efficiency step-down DC/DC<br>Price: ~$2–$6<br>[Product Page](https://www.digikey.com/en/products/filter/dc-dc-converters/882)<br>![Buck Module](Thing_2.png) | • High efficiency → runs cool from 12 V<br>• Handles higher load current<br>• Wide input range and adjustable output | • Switching ripple/noise requires filtering<br>• PCB layout and EMI critical<br>• More components; taller height |
| **Option 3 — MCP1825S-5002 (5 V LDO)** <br>1 A LDO, lower dropout than 7805<br>Price: ~$1–$2<br>[Product Page](https://www.digikey.com/en/products/detail/microchip-technology/MCP1825S-5002E-AB/1505941)<br>![MCP1825S](Thing_3.png) | • Lower dropout than 7805<br>• Quieter output than buck<br>• Simple BOM | • Still linear → wastes heat<br>• 1 A limit<br>• Thermal design needed above a few hundred mA |

**Choice:** Option 1 — LM7805  
**Rationale:** We choose the LM7805 linear regulator based on providing a stable, low-noise 5 V output to be used for powering sensitive analog circuits or microcontrollers. Its two-capacitor application provides minimal required external parts and a straightforward PCB footprint, thus lowering the design complexity and potential points of failure on the PCB. Having used the LM7805 already in previous course work throughout the semester, the design team is accustomed to its behavior — less risky at stages of layout and debugging. Switching regulators (buck modules) might yield much higher efficiencies and lower power dissipation, particularly if the conversion is between 9 V or 12 V and 5 V, but such systems also present switching noise, require a careful PCB layout and filtering, and contribute additional complexity, which might not be justified for a fairly small current draw (1.5 A max). That noise could interfere with analog signals (e.g., from sensors).

---

## 2. Temperature Sensor (Analog Output)

| Solution | Pros | Cons |
|-----------|------|------|
| **Option 1 — LM20BIM7X/NOPB (analog, SC-70-5 SMT)** <br>TO-92 or SOIC<br>Price: ~$0.81<br>[TI Product Page](https://www.digikey.com/en/products/detail/texas-instruments/LM20BIM7X-NOPB/366749?msockid=2b2475af6c1d6d1102ad67846d8e6cef)<br>![LM35](op1.png) | • Better accuracy than many basic analog sensors, about ±1.5°C typical<br>• Analog output works well with a PIC ADC<br>• Surface-mount SC-70-5 package | • Still an analog sensor, so noise can affect readings<br>• Output scaling is less straightforward than a simple 10 mV/°C sensor, about 11.77 mV/°C<br>• Small package can be harder to hand-solder |
| **Option 2 — TMP1075DGKT** <br>2.7–5.5 V supply (750 mV @ 25 °C)<br>Price: ~$1.03<br>[Product Page](https://www.digikey.com/en/products/detail/texas-instruments/TMP1075DGKT/9597135)<br>![TMP36](T_sense.png) | • Digital I²C/SMBus interface<br>• Low power consumption<br>• Wide temp range (-55°C ~ 125°C) | •Limited measurement resolution compared to newer sensors<br>• Requires microcontroller communication<br>• Not ideal for extremely fast temperature changes |
| **Option 3 — MCP9700AT-E/TT** <br>Slope 10 mV/°C with 500 mV offset<br>Price: < $0.48<br>[Product Page](https://www.digikey.com/en/products/detail/microchip-technology/MCP9700AT-E-TT/1228267?msockid=2b2475af6c1d6d1102ad67846d8e6cef)<br>![MCP9700](op3.png) | • Simple 10 mV/°C analog output<br>• Low cost and easy to interface with a microcontroller ADC<br>• True surface-mount SOT-23-3 package | • Requires ADC conversion and software scaling in the microcontrolle<br>•Lower accuracy than some digital temperature sensorsl<br>• Analog output is still susceptible to noise/EMI |

**Choice:** Option 2 — TMP1075DGKT  
**Rationale:** The TMP1075DGKT was selected because of Its I²C/SMBus interface allows temperature data to be read directly by the MCU without needing analog-to-digital conversion, which improves measurement consistency and reduces the effect of noise compared to analog sensors. The sensor also has low power consumption and a wide operating temperature range, making it suitable for reliable use in different conditions. Although it requires microcontroller communication and software setup, its digital output, compact package, and stable performance make it the best choice for accurate temperature sensing in this design.

---

## 3. Barrel Jack

| Solution | Pros | Cons |
|-----------|------|------|
| **Option 1 —  PJ-006A-SMT-TR** <br>Price: ~$0.95/unit<br>[Product Page](https://www.digikey.com/en/products/detail/same-sky-formerly-cui-devices/PJ-006A-SMT-TR/408456) <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/7322b12c-4f87-4b09-8c01-1bb6030f3f31" /> | • Standard barrel jack<br>• Sufficient for application<br>• Simple to install | • Shipping fee<br>• Shipping fee<br>• Must ensure correct polarity |
| **Option 2 — PJ-006B-SMT-TR** <br>Price: ~ $0.95/unit <br>[Product Page](https://www.digikey.com/en/products/detail/same-sky-formerly-cui-devices/PJ-006B-SMT-TR/408457) <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/8378c194-9761-4f94-acf5-dcb0bdc55573" /> | • Standard barrel connector size<br>• Handles moderate power levels<br>• Standard barrel connector size | • Limited current capacity compared to larger connectors<br>• Mechanical stress on SMT pads<br>• Requires specific barrel plug size |
| **Option 3 — PJ-102AH-SMT-TR** <br>Price: ~$0.85/unit<br>[Product Page](https://www.digikey.com/en/products/detail/same-sky-formerly-cui-devices/PJ-102AH-SMT-TR/10247683)![5mm LED](pj.png) | • Surface-mount package compatible with PCB assembly<br>• Standard 5.5 mm / 2.1 mm barrel connector size<br>• Compact footprint for small PCB layouts | • SMT pads can experience mechanical stress from repeated plug use<br>• Limited current compared to larger power connectors<br>• Requires correct barrel plug size for proper contact |

**Choice:** Option 1 – PJ-006A-SMT-TR

**Rationale:** The PJ-006A-SMT-TR barrel jack was selected because it provides a reliable and simple method for supplying external DC power to the system. This connector supports standard 5.5 mm barrel plugs and can handle the moderate voltage and current levels required for the project’s 5 V regulated power system. Its surface-mount design allows it to be easily integrated into the PCB layout while maintaining a compact footprint. Additionally, the connector is inexpensive, widely available, and easy to use with common DC adapters, making it a practical choice for prototyping and testing. The straightforward two-contact design also simplifies wiring and reduces the chance of incorrect polarity connections when used with a regulated power supply.

---
## 4. Red LED Indicator (5 V MCU Pin + Resistor)

| Solution | Pros | Cons |
|-----------|------|------|
| **Option 1 – LTST-C150KRKT (SMD Red LED)** <br>Vf ≈ 2.0 V typical @ 20 mA<br>Price: < $0.10<br>[Digikey Page](https://www.digikey.com/en/products/detail/lite-on-inc/LTST-C150KRKT/386800)<br>![LTST-C150KRKT LED](ltst.png) | • Small surface-mount footprint (0603 package)<br>• Low forward voltage suitable for 5 V logic systems<br>• Good brightness for indicator applications | • Very small size makes hand-soldering difficult<br>• Less visible than larger LED packages<br>• Requires current-limiting resistor |
| **Option 2 — 0805 SMD Red LED**<br>Vf ≈ 2.0 V typical<br>Price: < $0.10<br>[Digikey Page](https://www.digikey.com/en/products/filter/led-indication-discrete/105)<br>![0805 LED](Thing_11.png) | • Compact for tight PCBs<br>• Suited for reflow assembly<br>• Low parasitics | • Tricky to hand-solder<br>• Less visible off-axis<br>• Needs silkscreen polarity |
| **Option 3 — 1206 SMD Red LED**<br>Vf ≈ 2.0 V typical<br>Price: < $0.10<br>[Mouser Page](https://www.mouser.com/c/optoelectronics/leds/standard-leds-single-color/)<br>![1206 LED](Thing_13.png) | • Bigger pads (easier hand-solder)<br>• Still compact<br>• Good visibility | • Needs resistor & stencil<br>• Slightly larger area<br>• Taller profile |
 
**Choice:** Option 1 — 5 mm Red LED (THT) 
**Rationale:** I chose to utilize a 5 mm through-hole (THT) red LED as it is bright and can be visible from different directions — which is good for your user experience for status indications or alerts. For a development or proof-of-concept board, visibility is often more critical than compactness, and THT LEDs can certainly serve as a practical aid for debugging, early prototype, or demonstration builds. The through-hole form factor also makes soldering and rework for prototypes or low-volume builds easier, and the components can be replaced and/or adjusted by hand if they need to be replaced or modified.

---

## 5. Button (User Interface Subsystem)

| Solution | Pros | Cons |
|-----------|------|------|
| **Option 1 — PTS645SL43-2 LFS Tactile Switch**<br>Basic push button, low cost, easy to integrate<br>Price: $0.24/each<br>[Product Page](https://www.digikey.com/en/products/detail/c-k/PTS645SL43-2-LFS/1146755)<br>[Datasheet](https://www.ckswitches.com/media/1471/pts645.pdf)<br>![PTS645SL43-2LFS](PTS645SL43-2LFS%20(1).jpeg) | • Very low cost<br>• Easy to use | • Short lifespan<br>• Less tactile feedback |
| **Option 2 — Omron B3F Series Tactile Switch**<br>High-quality tactile push button, reliable, long life<br>Price: $0.24/each<br>[Product Page](https://www.digikey.com/en/products/detail/omron-electronics-inc-emc-div/B3F-1000/33150)<br>[Datasheet](https://omronfs.omron.com/en_US/ecb/products/pdf/en-b3f.pdf)<br>![B3F](B3F%20(1).jpeg) | • Long lifespan (~1M presses)<br>• Reliable actuation<br>• Consistent tactile feel | • Slightly higher cost<br>• Requires careful soldering |
| **Option 3 — Adafruit Mini Tactile Switch**<br>Compact, low profile, low cost<br>Price: $0.75/each<br>[Product Page](https://www.adafruit.com/product/367)<br>[Datasheet](https://cdn-shop.adafruit.com/datasheets/B3F-1000-Omron.pdf)<br>![Adafruit Mini](Adafruit_mini_tactile%20(1).jpg) | • Compact<br>• Low cost<br>• Easy to use | • Shorter lifespan<br>• Less tactile feel |

**Choice:** Option 2 — Omron B3F Series Tactile Switch  
**Rationale:** We included the Omron B3F tactile switch due to a high-quality tactile feel, a reliable actuation, and a long lifetime (on the order of 1 million actuations). For a user interface — where human interaction, button press feel, and durability matter — these features show a substantial difference in usability and user satisfaction. A button that feels cheap or fails after a few uses can really degrade the perceived quality of the product. Though there are also cost-effective competitors like simple tactile switches or compact mini-switches, these alternatives can often cause poor tactile feedback, inconsistency in the actuation force applied, shorter lifespan, and potentially unreliable switching over time. Even for a project that might be heavily tested through manual testing, debugging, or user interaction (particularly in a lab or classroom), this can be a major drawback.



## Final Major Components Selected 

| Solution | Pros | Cons |
|-----------|------|------|
| **7805 Linear Regulator (TO-220)**<br>Dropout ≈ 2 V<br>Simple 2-capacitor application<br>Price: ~$1–$2 (qty 1)<br>[Product Page](https://www.digikey.com/en/products/filter/linear-voltage-regulators/699)<br>![LM7805](Thing_1.png) | • Very simple and low-noise output<br>• Easy to source and short lead time<br>• Excellent line/load regulation | • Inefficient from 12 V → 5 V<br>• Needs heatsink above ~300 mA<br>• Dropout ≈ 2 V limits low-Vin |
| **TMP36 (analog with offset)**<br>2.7–5.5 V supply (750 mV @ 25 °C)<br>Price: ~$1–$2<br>[Analog Devices Page](https://www.analog.com/en/products/tmp36.html)<br>![TMP36](Thing_5.png) | • Works from 5 V rail<br>• Low power and easy ADC interface<br>• Wide temp range (−40 to 125 °C) | • Accuracy ±2 °C<br>• Offset must be subtracted in firmware<br>• Analog output needs filtering |
| **MCP6002 (dual, rail-to-rail I/O)**<br>1.8–5.5 V, 1 MHz GBW<br>Price: ~$0.50–$1.50<br>[Microchip Page](https://www.microchip.com/en-us/product/MCP6002)<br>![MCP6002](Thing_7.png) | • Rail-to-rail I/O at 5 V<br>• Low quiescent current<br>• Unity-gain stable | • Limited bandwidth (1 MHz)<br>• Modest slew rate<br>• Low output drive |
| **5 mm Red LED (THT)**<br>Vf ≈ 2.0 V @ 20 mA<br>Price: < $0.10<br>[Digikey Page](https://www.digikey.com/en/products/filter/led-indication-discrete/105)<br>![5mm LED](Thing_10.png) | • Bright and easy to see<br>• Breadboard-friendly<br>• Durable leads | • Large footprint<br>• Requires holes (through-hole)<br>• Protrudes above PCB |
| **Omron B3F Series Tactile Switch**<br>High-quality tactile push button, reliable, long life<br>Price: $0.24/each<br>[Product Page](https://www.digikey.com/en/products/detail/omron-electronics-inc-emc-div/B3F-1000/33150)<br>[Datasheet](https://omronfs.omron.com/en_US/ecb/products/pdf/en-b3f.pdf)<br>![B3F](B3F%20(1).jpeg) | • Long lifespan (~1M presses)<br>• Reliable actuation<br>• Consistent tactile feel | • Slightly higher cost<br>• Requires careful soldering |
| **Amazon Basics 9V 3A AC/DC Adapter (B09ZTKTLGW)**<br>![B09ZTKTLGW](206C2.png)<br>regulated output, compact wall-plug design<br>Price: $4.99/each<br>[Product Page](https://www.amazon.com/gp/product/B09ZTKTLGW/) | - Affordable and widely available<br>- Compact, plug-in wall adapter (saves space)<br>- Regulated output ensures stable voltage<br>- Includes standard barrel plug (5.5mm x 2.1mm)<br>- Suitable for continuous operation | - Lower build quality compared to industrial brands<br>- Limited protection features (no explicit overcurrent/short-circuit protection)<br>- Not designed for harsh environments or high-reliability applications<br>- May run warm under full load |
---
