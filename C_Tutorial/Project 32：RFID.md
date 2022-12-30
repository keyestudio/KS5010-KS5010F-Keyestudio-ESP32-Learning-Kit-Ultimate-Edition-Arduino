# Project 32：RFID

1. Introduction：

Nowadays, many residential districts use this function to open the
door by swiping the card, which is very convenient. In this Project,
we will learn how to use RFID(radio frequency identification)
wireless communication technology and read and write the key chain
card (white card) and control the steering gear rotation by
RFID-MFRC522 module.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:1.59722in;height:0.77986in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.75972in;height:1.8625in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/f12bee27e26177f00aa048f24499fc16.png" style="width:1.11667in;height:0.55278in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>RFID-RC522 Module*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/1fbdfe0569327d9a42600a54336bf7b5.png" style="width:1.38819in;height:1.15833in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/cd0bc424e9916881a1a903793821a042.png" style="width:1.25417in;height:1.04792in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/284218a1b5f1d347b1fd3c3119a34695.jpeg" style="width:0.64792in;height:0.98681in" /></td>
</tr>
<tr class="even">
<td>M-F Dupont Wires</td>
<td>Servo*1</td>
<td>White Card*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/284218a1b5f1d347b1fd3c3119a34695.jpeg" style="width:0.8in;height:0.92361in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e9a8d050105397bb183512fb4ffdd2f6.png" style="width:0.90694in;height:0.90139in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:0.99028in;height:0.52986in" /></td>
</tr>
<tr class="even">
<td>Key Chain*1</td>
<td>Jumper wires</td>
<td>USB Cable*1</td>
</tr>
</tbody>
</table>

3. Component knowledge：

**RFID：**RFID (Radio Frequency Identification) is a wireless
communication technology. A complete RFID system is generally composed
of the responder and reader. Generally, we use tags as responders, and
each tag has a unique code, which is attached to the object to identify
the target object. The reader is a device for reading (or writing) tag
information.

Products derived from RFID technology can be divided into three
categories: passive RFID products, active RFID products and semi active
RFID products. And Passive RFID products are the earliest, the most
mature and most widely used products in the market among others. It can
be seen everywhere in our daily life such as, the bus card, dining card,
bank card, hotel access cards, etc., and all of these belong to
close-range contact recognition. The main operating frequency of Passive
RFID products are: 125KHZ (low frequency), 13.56MHZ (high frequency),
433MHZ (ultrahigh frequency) and 915MHZ (ultrahigh frequency). Active
and semi active RFID products work at higher frequencies.

The RFID module we use is a passive RFID product with the operating
frequency of 13.56MHz.

**RFID-RC522 Module：**The MFRC522 is a highly integrated reader/writer
IC for contactless communication at 13.56MHz. The MFRC522's internal
transmitter is able to drive a reader/writer antenna designed to
communicate with ISO/IEC 14443 A/MIFARE cards and transponders without
additional active circuitry. The receiver module provides a robust and
efficient implementation for demodulating and decoding signals from
ISO/IEC 14443 A/MIFARE compatible cards and transponders. The digital
module manages the complete ISO/IEC 14443A framing and error detection
(parity and CRC) functionality.

This RFID Module uses MFRC522 as the control chip and adopts I2C
(Inter-Integrated Circuit) interface.

![](/media/5a19d0dd224c2cdc78871f11e8951045.png)

**Specifications:**

Operating voltage: DC 3.3V-5V

Operating current: 13—100mA/DC 5V

Idling current: 10-13mA/DC 5V

Sleep current: \<80uA

Peak current: \<100mA

Operating frequency: 13.56MHz

Maximum power: 0.5W

Supported card types: mifare1 S50, mifare1 S70, mifare UltraLight,
mifare Pro, mifare Desfire.

Environmental operating temperature: -20 to 80 degrees Celsius.

Environment storage temperature: -40 to 85 degrees Celsius.

Relative Humidity: 5% to 95%.

Data transfer rate: The maximum is 10Mbit/s.

4. RFID Read UID：

We will read the UNIQUE ID number (UID) of the RFID card and identify
the type of the RFID card, and display the relevant information through
the serial port. The wiring diagram is shown below：

![](/media/1cdb3ffd7f392f29451aeed5c3257133.png)

**Adding the MFRC522\_I2C and Wire libraries：**

If you haven't installed the **MFRC522\_I2C** and **Wire** libraries
yet, please do so before learning. The steps to add third-party
libraries are as follows:

Open the Arduino IDE，click“Sketch”→“Include Library”→“Add .ZIP
Library...”. In the pop-up window, find the file named **“2. Windows
System\\2. C\_Tutorial\\3.Libraries\\MFRC522\_I2C.ZIP”** which locates
in this directory. Select the MFRC522\_I2C.ZIPfile and then click“Open”.

![](/media/835a3d1d8e0e3003c3d12e12e909de64.png)

![](/media/9296c1f45b1e6e17e45c209b2aa2b68c.png)

Then, in the pop-up window, find the file named **“**2. Windows
System\\2. C\_Tutorial\\3.Libraries\\Wire.ZIP which locates in this
directory. Select the Wire.Zip file and then click“Open”.

![](/media/1f8d04a8dae6fc1e0dead079d36d0512.png)

After the **MFRC522\_I2C** and **Wire** libraries were added, you can
open the code we provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project
32：RFID\\Project\_32.1\_RFID\_Read\_UID”**.

    //**********************************************************************************
    /*  
     * Filename    : RFID
     * Description : RFID reader UID
     * Auther      : http//www.keyestudio.com
    */
    #include <Wire.h>
    #include "MFRC522_I2C.h"
    // IIC pins default to GPIO21 and GPIO22 of ESP32
    // 0x28 is the i2c address of SDA, if doesn't match，please check your address with i2c.
    MFRC522 mfrc522(0x28);   // create MFRC522.
    
    void setup() {
      Serial.begin(115200);           // initialize and PC's serial communication
      Wire.begin();                   // initialize I2C
      mfrc522.PCD_Init();             // initialize MFRC522
      ShowReaderDetails();            // dispaly PCD - MFRC522 read carder
      Serial.println(F("Scan PICC to see UID, type, and data blocks..."));
    }
    
    void loop() {
      // 
      if ( ! mfrc522.PICC_IsNewCardPresent() || ! mfrc522.PICC_ReadCardSerial() ) {
        delay(50);
        return;
      }
      
      // select one of door cards. UID and SAK are mfrc522.uid.
      
      // save UID
      Serial.print(F("Card UID:"));
      for (byte i = 0; i < mfrc522.uid.size; i++) {
        Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
        Serial.print(mfrc522.uid.uidByte[i], HEX);
      } 
      Serial.println();
    }
    
    void ShowReaderDetails() {
      //  attain the MFRC522 software
      byte v = mfrc522.PCD_ReadRegister(mfrc522.VersionReg);
      Serial.print(F("MFRC522 Software Version: 0x"));
      Serial.print(v, HEX);
      if (v == 0x91)
        Serial.print(F(" = v1.0"));
      else if (v == 0x92)
        Serial.print(F(" = v2.0"));
      else
        Serial.print(F(" (unknown)"));
      Serial.println("");
      // when returning to 0x00 or 0xFF, may fail to transmit communication signals
      if ((v == 0x00) || (v == 0xFF)) {
        Serial.println(F("WARNING: Communication failure, is the MFRC522 properly connected?"));
      }
    }
    //**********************************************************************************


Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable, and open the serial monitor and
then set baud rate to 115200. You will see that place the door card and
key chain close to the module sensor area respectively, the serial
monitor display the card number and key chain value respectively, as
shown below:

![](/media/bbbeffbb074de316656963281cdb4943.png)

**Note:** the door card value and key chain value may be different for
different RRFID -RC522 door cards and key chains.

5. Wiring diagram of the RFID MFRC522：

Now we use the RFID -RC522 module, white card/key chain and Servo to
simulate an intelligent access control system. When the white
card/key chain close to the RFID -RC522 module induction area, the
servo rotates. Wiring according to the figure below：

![](/media/3ae6c0f1098d2aee34c51e7a96c25571.png)

6. Adding the MFRC522\_I2C, Wire and ESP32Servo libraries：

The **MFRC522\_I2C**, **Wire** and **ESP32Servo** libraries had been
added previously, so you don't need to add it again. If not, you need to
add the **MFRC522\_I2C**, **Wire** and **ESP32Servo** libraries. The
steps to add third-party libraries are as follows:

First, add the **ESP32Servo** library：

Open the Arduino IDE，click“Sketch”→“Include Library”→“Add .zip
Library...”. In the pop-up window, find the file named **“2. Windows
System\\2. C\_Tutorial\\3.Libraries\\ ESP32Servo-0.8.0.Zip”** which
locates in this directory. Select the ESP32Servo-0.80.Zipfile and then
click “Open”.

![](/media/8d580f9d67946706c0b184b5953ca89a.png)

![](/media/7821c38a6056ac77c2917080e9f557b1.png)

Then, add the **MFRC522\_I2C** and **Wire** libraries：

If both of them are added, just skip this step.

7. Project code：

After the **MFRC522\_I2C**、**Wire** and **ESP32Servo** libraries were
added, you can open the code we provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project
32：RFID\\Project\_32.2\_RFID\_Control\_Servo”**.

**Note:** Different RFID-MFRC522 IC cards and keys have diverse
values.You can substitute your own IC cards and keys values for the
corresponding values read by the RFID-MFRC522 module in the program,
otherwise the servo can’t be controlled when uploading the test code to
the ESP32.

For example: You can replace the rfid\_str of the
![](/media/85170ea6c47d9350dd05efa60be8c808.png) in the program code with your own IC cards and
keys values read by the RFID-MFRC522 module.

    //*************************************************************************************
    /* 
     * Filename    : RFID mfrc522 Control Servo
     * Description : RFID controlled steering gear simulated door opening
     * Auther      : http//www.keyestudio.com
    */
    #include <Wire.h>
    #include "MFRC522_I2C.h"
    // IIC pins default to GPIO21 and GPIO22 of ESP32
    // 0x28 is the i2c address of SDA, if doesn't match，please check your address with i2c.
    MFRC522 mfrc522(0x28);   // create MFRC522.
    
    #include <ESP32Servo.h>
    Servo myservo;  // create servo object to control a servo
    int servoPin = 15; // Servo motor pin
    
    String rfid_str = "";
    
    void setup() {
      Serial.begin(115200);
      Wire.begin();
      mfrc522.PCD_Init();
      ShowReaderDetails();            // dispaly PCD - MFRC522 read carder
      Serial.println(F("Scan PICC to see UID, type, and data blocks..."));
      
      myservo.setPeriodHertz(50);           // standard 50 hz servo
      myservo.attach(servoPin, 500, 2500);  // attaches the servo on servoPin to the servo object
      myservo.write(0); 
      delay(500);
    }
    
    void loop() {
       if ( ! mfrc522.PICC_IsNewCardPresent() || ! mfrc522.PICC_ReadCardSerial() ) {
        delay(50);
        return;
      }
      
      // select one of door cards. UID and SAK are mfrc522.uid.
      
      // save UID
      rfid_str = ""; //String emptying
      Serial.print(F("Card UID:"));
      for (byte i = 0; i < mfrc522.uid.size; i++) {
        rfid_str = rfid_str + String(mfrc522.uid.uidByte[i], HEX);  //Convert to string
        //Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
        //Serial.print(mfrc522.uid.uidByte[i], HEX);
      } 
      Serial.println(rfid_str);
      
      if (rfid_str == "93adf720" || rfid_str == "39b646c2") {
        myservo.write(180);
        delay(500);
        Serial.println("  open the door!");
        }
    }
    
    void ShowReaderDetails() {
      //  attain the MFRC522 software
      byte v = mfrc522.PCD_ReadRegister(mfrc522.VersionReg);
      Serial.print(F("MFRC522 Software Version: 0x"));
      Serial.print(v, HEX);
      if (v == 0x91)
        Serial.print(F(" = v1.0"));
      else if (v == 0x92)
        Serial.print(F(" = v2.0"));
      else
        Serial.print(F(" (unknown)"));
      Serial.println("");
      // when returning to 0x00 or 0xFF, may fail to transmit communication signals
      if ((v == 0x00) || (v == 0xFF)) {
        Serial.println(F("WARNING: Communication failure, is the MFRC522 properly connected?"));
      }
    }
    //*************************************************************************************


8. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable, and open the serial monitor
and then set baud rate to 115200. You will see that when using the
white card or a key card swiping, the serial port monitor displays
white card or key card information and “open the door”. As shown in
the picture below, and the servo rotates to the corresponding angle
to simulate opening the door.

![](/media/3a125fc98b567c34b02285caf111e3f1.png)
