# Project 29：Temperature Humidity Meter 

1. Introduction：

In winter, the humidity in the air is very low, that is, the air is very
dry, Coupled with cold, the skin of the human body is easy to be too dry
and cracked, so you need to use a humidifier to increase the humidity of
the air at home, but how do you know that the air is too dry? Then you
need equipment to detect air humidity. In this Project, we will how to
use the temperature and humidity sensor. We use the sensor to make a
thermohygrometer, and also combined with a LCD 128X32 DOT to display the
temperature and humidity values.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:1.59722in;height:0.77986in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.70139in;height:1.71944in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/34bafe8113e2db36c8f0c8492b835474.png" style="width:1.27292in;height:0.96111in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>Temperature and Humidity Sensor*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/9232141f8a3166a8a6cdd43b78edd4e3.png" style="width:1.29722in;height:0.625in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/f1aed48e2c02214415853ad2358f3744.png" style="width:0.97569in;height:0.82431in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.275in;height:0.68264in" /></td>
</tr>
<tr class="even">
<td>LCD 128X32 DOT*1</td>
<td>M-F Dupont Wires</td>
<td>USB Cable*1</td>
</tr>
</tbody>
</table>

3. Component knowledge：

![](/media/34bafe8113e2db36c8f0c8492b835474.png)

**Temperature and humidity sensor:** It is a temperature and humidity
composite sensor with calibrated digital signal output, its precision
humidity is±5%RH, temperature is±2℃, range humidity is 20 to 90%RH, and
temperature is 0 to 50℃. The temperature and humidity sensor applies
dedicated digital module acquisition technology and temperature and
humidity sensing technology to ensure extremely high reliability and
excellent long-term stability of the product. The temperature and
humidity sensor includes a resistive-type humidity measurement and an
NTC temperature measurement component, which is very suitable for
temperature and humidity measurement applications where accuracy and
real-time performance are not required.

The operating voltage is in the range of 3.3V to 5.5V.

The temperature and humidity sensor has three pins, which are VCC、GNDand
S. S is the pin for data output, using serial communication.

**Single bus format definition of Temperature and Humidity Sensor：**

    //**********************************************************************************
    /*
     * Filename    : Temperature and Humidity Sensor
     * Description : Use XHT11 to measure temperature and humidity.Print the result to the serial port.
     * Auther      : http//www.keyestudio.com
    */
    #include "xht11.h"
    //gpio13
    xht11 xht(13);
    
    unsigned char dht[4] = {0, 0, 0, 0};//Only the first 32 bits of data are received, not the parity bits
    void setup() {
      Serial.begin(115200);//Start the serial port monitor and set baud rate to 115200
    }
    
    void loop() {
      if (xht.receive(dht)) { //Returns true when checked correctly
        Serial.print("RH:");
        Serial.print(dht[0]); //The integral part of humidity, DHT [0] is the fractional part
        Serial.print("%  ");
        Serial.print("Temp:");
        Serial.print(dht[2]); //The integral part of temperature, DHT [3] is the fractional part
        Serial.println("C");
      } else {    //Read error
        Serial.println("sensor error");
      }
      delay(1000);  //It takes 1000ms to wait for the device to read
    }
    //**********************************************************************************


**Data sequence diagram of Temperature and Humidity Sensor：**

When MCU sends a start signal, the Temperature and Humidity Sensor
changes from the low-power-consumption mode to the high-speed mode,
waiting for MCU completing the start signal. Once it is completed, the
Temperature and Humidity Sensor sends a response signal of 40-bit data
and triggers a signal acquisition. The signal is sent as shown in the
figure:![](/media/933ac5e5a5e921d4b16c7c48091ba75a.png)

Combined with the code, you can understand better.

The XHT11 temperature and humidity sensor can easily add temperature and
humidity data to your DIY electronic projects. It is perfect for remote
weather stations, home environmental control systems, and farm or garden
monitoring systems.

**Specification:**

Working voltage: +5V

Temperature range: 0°C to 50°C, error of ± 2°C

Humidity range: 20% to 90% RH,± 5% RH error

Digital interface

**Schematic diagram of** **Temperature and Humidity Sensor:**

![](/media/53fa034cbbcec22579b2bdf8252c90cd.emf)

4. Read temperature and humidity value：

![](/media/5d6dd3f19b4323d212bb95e3e4d43743.png)

**How to add the xht11 library：**

This code uses a library named "**xht11**", if you haven't installed it
yet, please do so before learning. The steps to add third-party
libraries are as follows:

Open the Arduino IDE，click“Sketch”→“Include Library”→“Add .zip
Library...”. In the pop-up window, find the file named **“2 Windows
System\\2. C\_Tutorial\\3.Libraries\\xht11.ZIP”** which locates in this
directory. Select the **xht11.ZIP** file and then click“Open”.

![](/media/02cfe65a5dde15adcf39e0814235d4ed.png)

![](/media/e6d2e9f9b575f99bf4194a620f1b5dc3.png)

After the **xht11** library was added, you can open the code we provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 29：****Temperature Humidity
Meter\\Project\_29.1\_Detect\_Temperature\_Humidity”**.

    //**********************************************************************************
    /*
     * Filename    : Temperature Humidity Meter
     * Description : LCD displays the value of temperature and humidity.
     * Auther      : http//www.keyestudio.com
    */
    #include "xht11.h"
    #include "lcd128_32_io.h"
    
    //gpio13
    xht11 xht(13);
    unsigned char dht[4] = {0, 0, 0, 0};//Only the first 32 bits of data are received, not the parity bits
    
    lcd lcd(21, 22); //Create lCD128 *32 pin，sda->21， scl->22
    
    void setup() {
      lcd.Init(); //initialize
      lcd.Clear();  //clear
    }
    char string[10];
    
    //lcd displays humidity and temperature values
    void loop() {
      if (xht.receive(dht)) { //Returns true when checked correctly
        }
      lcd.Cursor(0,0); //Set display position
      lcd.Display("Temper:"); //Setting the display
      lcd.Cursor(0,8);
      lcd.DisplayNum(dht[2]);
      lcd.Cursor(0,11);
      lcd.Display("C");
      lcd.Cursor(2,0); 
      lcd.Display("humid:");
      lcd.Cursor(2,8);
      lcd.DisplayNum(dht[0]);
      lcd.Cursor(2,11);
      lcd.Display("%");
      delay(200);
    }
    //**********************************************************************************


Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable, and open the serial monitor and
then set baud rate to 115200. You will see the current temperature and
humidity value detected by the sensor from the serial monitor. As shown
in the following figure:

![](/media/117fc71bbd32402b68e6ff401246cbdf.png)

5. Wiring diagram of the thermohygrometer：

Now we start to print the values of the temperature and humidity sensor
with LCD\_128X32\_DOT. We will see the corresponding values on the
screen of LCD\_128X32\_DOT. Let's get started with this project. Please
connect cables according to the following wiring diagram：

![](/media/6c82bb28bd1fcd7a1f72108e8a4a70b6.png)

6. Project code：

The **xht11** and **lcd128\_32\_io** libraries have been added
previously, so you don't need to add them again. If not, you need to
add **xht11** and **lcd128\_32\_io** libraries. For the method of
adding the **xht11** library, please refer to the above method of
this Project, and for the method of adding the lCD128\_32\_IO
library, please refer to “Project 17: I2C 128 32 LCD”.

After the **xht11** and **lcd128\_32\_io** libraries were added, you can
open the code we provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 29：Temperature Humidity
Meter\\Project\_29.2\_Temperature\_Humidity\_Meter”**.

<table>
<tbody>
<tr class="odd">
<td><p>//*******************************************************************</p>
<p>/*</p>
<p>* Filename : Temperature Humidity Meter</p>
<p>* Description : LCD displays the value of temperature and humidity.</p>
<p>* Auther : http//www.keyestudio.com</p>
<p>*/</p>
<p>#include "xht11.h"</p>
<p>#include "lcd128_32_io.h"</p>
<p>//gpio13</p>
<p>xht11 xht(13);</p>
<p>unsigned char dht[4] = ;//Only the first 32 bits of data are received, not the parity bits</p>
<p>lcd lcd(21, 22); //Create lCD128 *32 pin，sda-&gt;21， scl-&gt;22</p>
<p>void setup() </p>
<p>char string[10];</p>
<p>//lcd displays humidity and temperature values</p>
<p>void loop() </p>
<p>lcd.Cursor(0,0); //Set display position</p>
<p>lcd.Display("Temper:"); //Setting the display</p>
<p>lcd.Cursor(0,8);</p>
<p>lcd.DisplayNum(dht[2]);</p>
<p>lcd.Cursor(0,11);</p>
<p>lcd.Display("C");</p>
<p>lcd.Cursor(2,0);</p>
<p>lcd.Display("humid:");</p>
<p>lcd.Cursor(2,8);</p>
<p>lcd.DisplayNum(dht[0]);</p>
<p>lcd.Cursor(2,11);</p>
<p>lcd.Display("%");</p>
<p>delay(200);</p>
<p>}</p>
<p>//*******************************************************************</p></td>
</tr>
</tbody>
</table>

**7.Project result：**

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that the LCD
128X32 DOT will display temperature and humidity value in the current
environment.
