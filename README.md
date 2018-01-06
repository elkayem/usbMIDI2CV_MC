# usbMIDI2CV_MC

![MIDI2CV](/images/IMG_1630.JPG)

<img src="/images/IMG_1623.JPG" alt="MIDI2CV" width="420" height="315"> <img src="/images/IMG_1631.JPG" alt="MIDI2CV" width="420" height="315">

This repository contains the code and schematics for a three-channel USB-MIDI to CV converter.  STL files are also included for a 3D printed case.  This project has the following features:
* Three channel Note CV output (88 keys, 1V/octave, MIDI channels 1-3) using a 12-bit DAC
* Configurable note priority for each channel (Top Note, Bottom Note, or Last Note Priority)
* Note scale factor calibration configurable in software
* 5V Gate/Trigger outputs, where each channel can be independently configured to either output a gate (output high for entire length of time that note is on) or trigger (20 msec pulse each time a new note is initiated)
* Velocity CV output (0 to 4V) for each channel
* Pitch Bend CV output (0.5 +/- 0.5V), which can be configured for channel 1, 2, or 3
* Control Change CV output (0 to 4V), which can be configured for channel 1, 2, or 3
* OLED user interface, used for setting parameters and saving to EEPROM

This module is the perfect interface between your computer or iPad and an analog synthesizer.  It can independently drive up to three oscillators with 1V/octave CV inputs.  (Connection to an iPad requires the USB camera adapter but is well worth it given the wide variety of great MIDI sequencer apps.)  

<img src="/images/IMG_1639.JPG" alt="MIDI2CV" width="420" height="315"> 

Note priority can be independengly set for each channel, with the following options:
* **Top Note (aka Highest Note):** When multiple notes are sounded simultaneously, the highest note being held will be sounded.  When the highest note is released, the next highest note will be played, and so on.
* **Bottom Note (aka Lowest Note):** Analagous to top note, except the lowest note being held will be sounded.  
* **Last Note:** The most recent note played will be sounded.  When that note is released, the next most recent note still being held will be sounded.  

The settings screen shows the current settings used.  Note priority is listed as sequence of three letters showing the setting for each of the three channels, where T = Top Note, B = Bottom Note, and L = Last Note.  Similarly, Gate/Trigger is listed as a sequence of three letters where G = Gate and T = Trigger.  Pitch Bend and CC settings show which MIDI channel will be used for the analog output.  Note scale factor can also be calibrated by +/-10%.  All of these settings can be set through the OLED interface using the encoder knob.

<img src="/images/IMG_1645.JPG" alt="MIDI2CV" width="420" height="315"> <img src="/images/IMG_1644.JPG" alt="MIDI2CV" width="420" height="315">

## Parts List
* Teensy 2.0
* 128x64 OLED graphic display, with I2C interface 
* Pushbutton Rotary encoder with knob (should have 5 pins)
* 4x MCP4822 12-bit DACs (8 pin DIP)
* 2x LM324N Quad Op Amp (14 pin DIP)
* 7x 0.1 uF ceramic capacitors
* 0.33 uF capacitor
* 3x 3K resistors (1% metal film)
* 3x 4.7K resistors (1% metal film)
* 3x 10K resistors (1% metal film)
* 3x 2K resistors
* 4x 8 pin DIP IC sockets
* 2x 14 pin DIP IC sockets
* 2x 12-pin female headers
* 8x banana jacks
* 3x 1/4" mono phone jacks
* (Optional) 2-pin 5.08mm pitch screw terminal, for power input 
* Barrel power jack (e.g., 2.1 x 5.5 mm)
* 9 - 12V DC power supply with barrel connector (e.g., 2.1 x 5.5 mm)
* PCB (Gerber files included) or strip board
* 6x 10mm M3 bolts and nuts (4 for panel, 2 for USB port)
* 4x M2 bolts and nuts for mounting the OLED screen
* Panel mount USB 2.0 USB Mini B Female to USB Mini B Male, 1 ft cable (see picture below)

<img src="/images/IMG_1620.JPG" alt="MIDI2CV" width="420" height="315"> 

## Instructions
Electronic components can be soldered to a strip board or (more conveniently) to the PCB design I have included in this repository.  I recommend using IC sockets to mount the ICs and female headers to mount the Teensy.  The PCB can be manufactured by a PCB supplier.  The least expensive way to do this is to upload the gerber files (included as a .zip file) to one of several Chinese manufacturers such as SchenZhen2U, EasyEDA, or Seeed Studio.  pcbshopper.com allows a comparison between vendors.  Typical prices are $1-$3/board, with a minimum of 5 boards.  Recommended default settings are Layers: 2; PCB Thickness: 1.6mm; Surface Finish: HASL; Copper Weight: 1.  (Alternatively, contact me since I may still have a few extras I could send out for $5 + shipping.)

<img src="/images/IMG_1619.JPG" alt="MIDI2CV" width="420" height="315"> <img src="/images/IMG_1622.JPG" alt="MIDI2CV" width="420" height="315">

**Important!** Before connecting the Teensy 2.0 to an external power supply, the 5V pads must be cut on the bottom side of the board.  See https://www.pjrc.com/teensy/external_power.html for details.

The 3D printer STL files are located in the 3D Printer Files folder. I've also included the Sketchup file, in case modifications are needed.  (Download Sketchup Make, it's free!) The panel includes raised text, and so must be printed with two colors. Most slicers include a "pause at height" plugin, which will move the hot end out of the way and allow you to switch filaments. The panels are 3mm thick, and the letters are 0.45mm thick. I printed with 0.15mm layer thickness, allowing the letters to be printed in three layers. Add the command to pause after you finish printing the 3mm layer, so you can change the filament color. (One tip: If you find that your printer is disabling the stepper motors after pausing, you may need to insert M84 S0 at the start of the G-Code. I did.)  

The 3D printed panel must be printed with supports for the OLED screen mount. There is a recessed area on the back side of the panel that fits the screen mounting shape. I recommend picking up the screen by DIYMall, as the hole pattern was designed for that screen. Others may fit as well. Supports are not required for the case.

I have included 1/4" jacks for the CV note outputs to ensure that the analog synthesizer shares a common ground with the MIDI2CV component.  Ground is carried over the sleeve.  The sleeve pins on the phone jacks need to be tied together, and then tied to a ground location on the PCB.  I did not provide a dedicated ground location on the PCB for this connection, but any location on the PCB will work.  (e.g., directly to the power ground input).  I left the remainder of the outputs as banana jacks assuming at least one of the notes is connected.  If desired, the banana jacks can be replaced with phone jacks.  Be aware that the holes in the 3D printed case may need to be enlarged, and and the case may need to be made taller to accomodate the depth of the additional phone jacks. 

The rotary encoder should have three pins on one side and two on the other.  Connect the three pins to the 3 ENC headers on the board, and the two pins to the 2 BTN pins on the board.  These may be connected using jumper wires and male header pins, or soldered directly to the board.

The OLED attaches to the I2C output on the PCB (marked as 5V, GND, SCL, SDA).  Note the pin order!  This order matches a commonly available OLED from DIYMall, but other OLEDs exist with the power and ground swapped.  Swapping power and ground will destroy the OLED.

The firmware can be uploaded to the Teensy 2.0 using the Teensy loader.  See https://www.pjrc.com/teensy/first_use.html for details.  The hex file is included in this repository.  If modification of the source code is required (e.g., for calibration as described below), then the Arduino software and Teensyduino must also be installed (see https://www.pjrc.com/teensy/td_download.html).  Several libraries are used, which are included as part of the Teensyduino installer.  Be sure to configure the board as Teensy 2.0 (under Tools > Board), and USB Port as MIDI (under Tools > USB Type).

**Important Note if recompiling firmware:**  In the file Adafruit_SSD1306.h (found either in the folder Arduino\libraries\Adafruit_SSD1306, where "Arduino" is your top level Arduino directory, or in the folder Arduino\hardware\teensy\avr\libraries), uncomment the line #define SSD1306_128_64, and comment out all other displays. If you don't do the above step, the library will assume you are using a 32-pixel display and the displayed text will not fit on the screen.

If using 1% metal film resistors, the MIDI2CV is likely to be in tune for the entire 7.25 octave (88 key) range.  The DAC output range is 4.096 V, which is amplified by 7.25/4.096 = 1.7700.  This is accomplished with the combination of 3K, 4.7K, and 10K resistors in the op-amp circuit.  (Note 3.01K is also common, and can be used.)  

If the MIDI2CV output scale factor isn't exactly 1V/octave, the scale factor can be adjusted by +/-10% using the user interface.  Mine was fairly close for all three channels, and required adjustment of only a few tenths of a percent. 
