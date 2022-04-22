The software serial library will allow us to use other pins than the default 0, 1 pins for the serial communication. Copy the code from the section below and upload it.


```#include <Adafruit_Fingerprint.h>

#include <LiquidCrystal_I2C.h>

#include <SPI.h>

#include <SoftwareSerial.h>

SoftwareSerial mySerial(2, 3);
```
In the setup function, set the baud rate at which the fingerprint sensor works. Then, check whether the fingerprint sensor is communicating with the Arduino or not.
```finger.begin(57600);

  if (finger.verifyPassword()) {

    lcd.setCursor(0, 0);
    lcd.print("  FingerPrint ");
    lcd.setCursor(0, 1);
    lcd.print("Sensor Connected");
  }

  else  
  
  {

    lcd.setCursor(0, 0);
    lcd.print("Unable to found");
    lcd.setCursor(0, 1);
    lcd.print("Sensor");
    delay(3000);
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Check Connections");

    while (1) {
      delay(1);
    }
  }
  ```
Now we need to set up your actual fingerprint! The following code section is for the user to place their finger on the fingerprint scanner that will convert the fingerprint into an image.

```uint8_t p = finger.getImage();
  if (p != FINGERPRINT_OK)  {
    lcd.setCursor(0, 0);
    lcd.print("  Waiting For");
    lcd.setCursor(0, 1);
    lcd.print("  Valid Finger");
    return -1;
  }

  p = finger.image2Tz();
  if (p != FINGERPRINT_OK)  {
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("  Messy Image");
    lcd.setCursor(0, 1);
    lcd.print("  Try Again");
    delay(3000);
    lcd.clear();
    return -1;
  }
p = finger.fingerFastSearch();
  if (p != FINGERPRINT_OK)  {
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Not Valid Finger");
    delay(3000);
    lcd.clear();
    return -1;
  }
  ```
If the image is messy, it will ask to scan your finger again in order to have a good fingerprint image that will be compared to the saved images of all the fingerprints in your system. Upon matching the image, the door will open. Otherwise, the door will remain closed.
![](https://maker.pro/storage/3BCXm1A/3BCXm1AMjEhXyK65ydqKaR6NFUhSAZ47t0jYsCjc.png)
Place your finger on the sensor so the system can create a picture of your fingerprint.

Once the system receives a clear fingerprint, your door lock is ready to use!
