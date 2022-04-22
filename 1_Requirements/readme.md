# INTRODUCTION:
Biometric systems have overtime served as robust security mechanisms in various domains. Fingerprints are the oldest and most widely used form of biometric identification. The use of fingerprint for identification has been employed in law enforcement for about a century. A much broader application of fingerprint is for personal authentication, for instance to access a computer, a network, an ATM machine, a car or a home.

Electronic lock using fingerprint recognition system is a process of verifying the fingerprint image to open the electronic lock. This project highlights the development of fingerprint verification. Verification is completed by comparing the data of authorized fingerprint image with incoming fingerprint image. Then the information of incoming fingerprint image will undergo the comparison process to compare with authorized fingerprint image.

Fingerprint door lock incorporates the proven technology. Fingerprint reader scanning is the most mature and tested type of biometric technology. Recent studies on biometrics have shown that compared to the hand method, fingerprint is more accurate and cost-effective. The duplication of biometric fingerprint technology is virtually impossible, only one in one billionth of a chance. Biometric security guarantees a positive method of user identification with something that cannot be lost, replicated or stolen.


# HIGH-LEVEL REQUIREMENTS:

we need some components for making this
## Arduino:
Arduino is an open-source electronics platform based on easy-to-use hardware and software. Arduino boards are able to read inputs - light on a sensor, a finger on a button, or a Twitter message - and turn it into an output - activating a motor, turning on an LED, publishing something online.
   
## fingerprint sensor:
The way this optical fingerprint sensor works is that it captures a photo of our finger ridges, and then it uses certain algorithm to match it with stored data and displays result of the same.

### Few features of this sensor are as following:

* Power supply: DC 3.8V-7.0V
* Operating current: 65mA (Typical)
* Interface: UART (TTL logical level)
* Average searching time: <1s (1:500, average)
* Security level: 5(1, 2, 3, 4, 5(highest))
* Working environment:Temp: -20°C to +60°
* Touch area dimension: 14.5*19.4 mm
* Outline dimension: 54*20*20.5 mm

## Relay module:
The relay module is an electrically operated switch that can be turned on or off deciding to let current flow through or not. They are designed to be controlled with low voltages like 3.3V like the ESP32, ESP8266, etc, or 5V like your Arduino

## solednoid lock:
In traditional door locks, there is a key to pull or push the latch, and we have to operate it manually. But on a solenoid lock, the latch can be operated automatically by applying some voltage. The solenoid lock contains a low-voltage solenoid that pulls the latch back to the door while an interrupt is activated (e.g. pushbutton, relay, etc.). The latch maintains its position until the interrupt is active. The operating voltage for the solenoid lock is 12V. You can also use 9V, but this results in slower operation. Solenoid door locks are mainly used to automate operations in remote areas without involving any human effort.
## R307 Digital fingerprint reader sensor

## Digital fingerprint reader:
![](https://hackster.imgix.net/uploads/attachments/1265548/ss_(1)_fMKeylHicQ.jpg?auto=compress%2Cformat&w=680&h=510&fit=max)

The biometric fingerprint sensor is ideal to create a system capable of protecting what you require through the analysis of your fingerprint. The device works with the serial protocol, so it can be used with any microcontroller (arduino etc..) or development card.

The device has the capacity to store up to 162 fingerprints in its internal FLASH memory. The device’s LED lights up every time it is taking pictures for fingerprints.
* Model: r307 
* Supply voltage: 5V
* Operation current: 100mA-150mA
* Fingerprint parity mode: 1: 1 1: n
* Baud rate: 9600 * NN = 1 to 12 (Default is 6)
* Acquisition time less than 1 second
* Security levels
* Window dimension: 14x18mm
* Working environment: -10 º c to 40 º c (Relative Humidity 40% to 85%)
* Dimensions: 5.5 x 2.1 x 2.0 cm Weight: 22g
To be able to use the device, it is necessary to save the fingerprints in its database. These footprints are assigned an ID. Subsequently, the reading and comparison sequence can be started to verify the fingerprints of the users and thus be able to discern and execute actions based on the result.


## what is inside in R307 fingerprint sensor:

* LEDs and touch sense pad

* TTP233D IC

* Remove the cap to see the prism

* Image sensor

* Fingerprint cross Section

* Schematic & circuit

* Arduino Fingerprint module D2 RX D3 TX GND GND 5v 5v

# LOW-LEVEL REQUIREMENTS:

* The sensor works at 57600 baud, it can be configured but this is the default speed, when using serial, the arduino uses the software serial library.

* #include <SoftwareSerial.h>
If it is required to change pins, the serial by software can be done in the following instruction:

* MySerial SoftwareSerial (2, 3);
For the example of the fingerprint, if the arduino is required to execute an action after having found a fingerprint, it is necessary to indicate it in this section of code:

* Serial.Print (“found ID #”);
* Serial.Print (Finger.fingerID);
* Serial.Print (“with confidence”);
* Serial.println (Finger.Confidence); Write the code here return finger.fingerID;
* We open the Arduino Serial Monitor to start recording the tracks and follow the instructions:

* We save the first fingerprint in position 1 and then we give it enter and follow the instructions:

* If the fingerprint was registered correctly, it will show the message “Fingerprint DOES match!”, followed by the position where it was saved and the message “Registered!”

* To save more than one fingerprint, the sensor allows up to 162 fingerprints, we now retype the number of the next position where we want to save it, which in this example would be position 2, we type 2 and press enterand continue again the same instructions until all the necessary footprints are recorded, always indicating a different position so that one already saved is not overwritten.

Finally we load the final program that will read the fingerprints. If the fingerprint read matches one of those stored, the relay that is connected to Pin 13 of the Arduino will be activated for 3 seconds
