# Open-Mouth-Mouse 

An open-source, affordable assistive technology project that enables computer control through mouth movements and sip/puff actions. This is an updated version of the original Mouth-Operated Mouse, that has been toughened up with a custom pcb and more robust case in order to be deployed for daily use by tetraplegics. This project was developed for the ParaWork team at the Swiss Paraplegic Centre in order to enable quick access to this type of assistive device, bypassing the need to involve insurance companies.

## Overview

This project creates a mouth-operated mouse combining a pressure sensor for sip/puff actions with a joystick for cursor movement, allowing users with limited hand mobility to control a computer. A keyboard mode is also included, where 2 to 8 keybinds are assigned to different angles, and special keys can be bound to sips and puffs. The mouse functions as follows:

*   **Joystick**: Controls cursor movement (operated by mouth)
*   **Sip/Puff Actions**: 
    *   Hard puff → Right click
    *   Soft puff → Scroll down
    *   Neutral → No action
    *   Soft sip → Scroll up
    *   Hard sip → Left click
These controls are inverted from the previous version because users requested it.

## Upgrades over the main V3

*   **Custom PCB**: The circuit now no longer needs to be completely hand soldered, only the components need to be attached.
*   **Improved case**: The case is now more robust and has a pressed in 1/4 nut to allow for attaching to standard camera mounts.

## Components

1.  **Arduino pro micro** (~$1 USD)
    *   Replaces Arduino Uno and Leonardo for direct HID capabilities and a more compact design.
    *   Pinout must match the SparkFun Electronics version in order to fit in PCB, there are many on aliexpress that fit this requirement.
2. **Custom PCB** (~$1 USD per board + $5-$20 shipping
    *   Hand the gerber files to one of the large manufacturers, the total price per delivered pcb obviously goes down as you order more, so consider doing a batch production.
3.  **NPA-500B-001G** (~$30 USD)
    *    - Specifically designed for sip/puff applications
         - I have tested another sensor but it didn't behave similarly to the NPA sensor, more testing needed to find the correct affordable version. This is where the most improvement in price can still be found.
4.  **PS4 Thumb Joystick** (~$1 USD)
    *   The PCB fits a PS4 thumb joystick, ideally choose a TMR magnetic version to allow for more precision and setting a smaller deadzone.
5.  **Tubing** (~$1 USD)
    *   Food-grade silicone tubing 1 meter - 2mm x 3mm 
6.  **3d Printed parts**
    *   Mouthpeice and Casing (Cost varies, ideally the maker has their own printer or access to one)
7.  **Soldering Components:**
    *   Basic soldering stuff, solder, flux (fluxed solder works too, make sure you have a fine tip)
    *   USB to USB-C cable for Arduino (~$1 USD)
    *   1uf electrolytic capacitor (~$0.1 USD)
8. **Small M3 Screws**
    *   Just some short m3 screws of any type
    
**Estimated Total Cost:** Approximately $40 USD not including shipping, cost varies from country to country and quantity of parts ordered.

## Setup Instructions

### 1. PCB Assembly

Follow this order for soldering to the board:

*   **Pressure sensor**
    *   Start with this as it will be difficult once the other components are attached.
    *   Follow [this tutorial](https://youtu.be/EW9Y8rDm4kE?si=filJ9XeB6xgZvDsz&t=374) to solder the pressure sensor, this is the trickiest part to do, just be patient and it will be fine.
    *   Dont forget to check that the orientation of the chip is correct by matching the dot in the corner to the one on the pcb.
    *   Even if only 3 pins are necessary for the sensor to function, you should still solder all of the pins otherwise it will be too weakly attached.
*   **Through hole components**
    *   Now you can solder all of the other components to the board, the order is not important. As they are all through-hole components the technique for doing so is the same for all of them [here is a tutorial](https://youtu.be/vAx89WhpZ3k?si=IwgAvfRAVOeoopeO) if you are unsure.
    *   Remember to connect the capacitor with correct polarity.

      
### 2. Arduino IDE Setup

1.  **Install Arduino IDE**: Download and install the Arduino IDE from the [official website](https://www.arduino.cc/en/software).
2.  **Install Arduino Pro Micro Board**: Go to `Tools > Board > Boards Manager...` and search for "Arduino AVR Boards". Install the package that includes the Arduino Leonardo.
3.  **Install Libraries**: The `V3.ino` sketch uses the built-in `Mouse.h` library. No additional library installations are required for the Arduino sketch.
4.  **Upload Sketch**: Open `V3.ino` in the Arduino IDE, select `Tools > Board > Arduino Pro Micro`, and choose the correct `Port`. Then, click `Upload`.

### 3. Case Assembly

*   **Lower Casing**
    *   Press the 1/4 nut into the hole in the lower casing, it should be set deep enough that the screw on whatever arm you are using can grab onto it.
    *   Place the PCB inside of the case with the joystick sitting above the nut.
    *   Fasten the PCB in place with 4 short m3 screws.
*   **Mouthpiece**
    *   Cut a piece of the silicon food-grade tubing about 10 cm long.
    *   Connect the tubing to the pressure port on the sensor, there are 2 pressure ports for most models, the one closer to the dot in the corner should be the one you connect to, the other one inverts sips and puffs.
    *   The other end of the tubing connects to the hole on the mouthpiece.
    *   Place the mouthpiece on the joystick.
    *   At this poimt the mouse should already be functional, plug it in and try it out to check. If not do the troubleshooting now before you close it up.
*   **Upper Casing**
    *   Temporarily remove the tube from the mouthpiece.
    *   Thread your tubing through the small hole on the top half of the casing.
    *   Then place the top case ontop of the lower and press it down.
    *   Fasten the parts together with 4 more m3 screws.
    *   Reattach the tube to the mouthpiece.

### 3. Python Application Setup

1.  **Install Python**: Ensure you have Python 3.x installed. You can download it from [python.org](https://www.python.org/downloads/).
2.  **Install Dependencies**: Open a terminal or command prompt and navigate to the directory where `App.py` is located. Install the required Python libraries using pip:
    ```bash
    pip install pyserial customtkinter pyautogui
    ```
3.  **Run Application**: Execute the Python application:
    ```bash
    python App.py
    ```
## Usage

Once the Arduino sketch is uploaded and the Python application is running, you can use the `App.py` interface to:

*   **Connect to Arduino**: Select the serial port connected to your Arduino Leonardo and click "Connect".
*   **Tune Parameters**: Adjust the pressure thresholds (Hard Sip, Neutral Min/Max, Soft Puff, Hard Puff) and joystick deadzone/cursor speed. Apply settings to the Arduino.
*   **Calibrate Sensor**: Use the "Calibrate Sensor" tab to visualize real-time pressure readings and fine-tune your thresholds for optimal performance.
*   **Train**: Utilize the "Trainer" tab to practice and improve your control.
*   **Manage Profiles**: Save and load different configurations as profiles.

## Troubleshooting

*   **Arduino Not Detected**: Ensure the Arduino Pro Micro drivers are correctly installed and the correct port is selected in the Arduino IDE and `App.py`.
*   **Serial Communication Issues**: Verify that no other application is using the serial port. Restarting the Arduino IDE or `App.py` might help.
*   **Mouse Not Moving/Clicking**: Check the pressure sensor and joystick connections. Ensure the `V3.ino` sketch is successfully uploaded to the Arduino Leonardo.
*   **Calibration**: The pressure thresholds are highly dependent on your specific sensor and lung capacity. Use the "Calibrate Sensor" tab in `App.py` to find your optimal settings.

## Link for video guide:

* Software: https://youtu.be/A-l-xfMGubU

## 🛠️ OSHWA Certification

This hardware project is certified by the [Open Source Hardware Association (OSHWA)](https://www.oshwa.org/).

**Certification UID**: [AU000021](https://certification.oshwa.org/au000021.html)
## Contributing

Contributions are welcome! Please feel free to fork the repository, make improvements, and submit pull requests. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is open-source and available under the [MIT License](https://opensource.org/licenses/MIT).
