# Project 31：Temperature Instrument

1. Introduction：

Thermistor is a kind of resistor whose resistance depends on
temperature changes, which is widely used in gardening, home alarm
system and other devices. Therefore, we can use the feature to make
a temperature instrument.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:1.59722in;height:0.77986in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.69306in;height:1.7in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/b45bb81bb3763377c63accce606ac5f2.png" style="width:0.25in;height:1.11597in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/b395b1cd2678f87b3a34dec15659efbc.png" style="width:0.22431in;height:1.00556in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>Thermistor*1</td>
<td>10KΩResistor*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/74ca4fa6d49dbd04de6a603c6e55a9ee.png" style="width:1.15347in;height:0.9625in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/9232141f8a3166a8a6cdd43b78edd4e3.png" style="width:1.52014in;height:0.73264in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e9a8d050105397bb183512fb4ffdd2f6.png" style="width:1.10139in;height:1.03472in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:0.99028in;height:0.52986in" /></td>
</tr>
<tr class="even">
<td>M-F Dupont Wires</td>
<td>LCD 128X32 DOT*1</td>
<td>Jumper Wires</td>
<td>USB Cable*1</td>
</tr>
</tbody>
</table>

3. Component knowledge：

**Thermistor:** A Thermistor is a temperature sensitive resistor. When
it senses a change in temperature, the resistance of the Thermistor will
change. We can take advantage of this characteristic by using a
Thermistor to detect temperature intensity. A Thermistor and its
electronic symbol are shown below:

![](/media/809b8634747fb295021f12e3b92b7894.png)

The relationship between resistance value and temperature of a
thermistor is：

**Where:**

**Rt** is the thermistor resistance under T2 temperature;

**R** is the nominal resistance of thermistor under T1 temperature;

**EXP\[n\]** is nth power of e;

**B** is for thermal index;

**T1, T2** is Kelvin temperature (absolute temperature). Kelvin
temperature=273.15 + Celsius temperature.

For the parameters of the Thermistor, we use: B=3950, R=10k, T1=25.

The circuit connection method of the Thermistor is similar to
photoresistor, as the following：

![](/media/b0f80e9bd350a8b7390a73756ac1ac8c.jpeg)

We can use the value measured by the ADC converter to obtain the
resistance value of Thermistor, and then we can use the formula to
obtain the temperature value.

Therefore, the temperature formula can be derived as:：

4. Read the value of the Thermistor：

First we will learn the thermistor to read the current ADC value,
voltage value and temperature value and print them out. Please connect
the wires according to the wiring diagram below：

![](/media/806fd81bf8a761b4ae1a638489c426ce.png)

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 31：Temperature
Instrument\\Project\_31.1\_Read\_the\_thermistor\_analog\_value”**.

    //**********************************************************************************
    /*  
     * Filename    : Thermomter
     * Description : Making a thermometer by thermistor.
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_ANALOG_IN   36
    void setup() {
      Serial.begin(115200);
    }
    
    void loop() {
      int adcValue = analogRead(PIN_ANALOG_IN);                       //read ADC pin
      double voltage = (float)adcValue / 4095.0 * 3.3;                // calculate voltage
      double Rt = 10 * voltage / (3.3 - voltage);                     //calculate resistance value of thermistor
      double tempK = 1 / (1 / (273.15 + 25) + log(Rt / 10) / 3950.0); //calculate temperature (Kelvin)
      double tempC = tempK - 273.15;                                  //calculate temperature (Celsius)
      Serial.printf("ADC value : %d,\tVoltage : %.2fV, \tTemperature : %.2fC\n", adcValue, voltage, tempC);
      delay(1000);
    }
    //**********************************************************************************


Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable, open the serial monitor and set
the baud rate to 115200. You will see that the serial port monitor
window prints out the thermistor's current ADC value, voltage value and
temperature value. Try pinching the thermistor with your index finger
and thumb (don't touch wires) for a while, and you will see the
temperature increase.

![](/media/0e4350465e1899e6eeee27b899a7f140.png)

5. Wiring diagram of the temperature instrument：

![](/media/5a437bfdcad012211e15cab54e35dad7.png)

**6. Adding the lcd128\_32\_io library：**

The **lcd128\_32\_io** library had been added previously, so you don't
need to add it again. If not, you need to add the **lcd128\_32\_io**
library. The steps to add third-party libraries are as follows:

Open the Arduino IDE，click “Sketch”→“Include Library”→“Add .ZIP
Library...”. In the pop-up window, find the file named **“2. Windows
System\\2. C\_Tutorial\\3. Libraries\\LCD\_128X32.ZIP”** which locates
in this directory. Select the **LCD\_128X32.ZIP** file and then click
“Open”.

![](/media/0936369979925135ae6fb54cbb9d4233.png)

![](/media/1ace99ef906441d1b7c6db48bda4930d.png)

**7. Project code：**

After the **lcd128\_32\_io** library was added, you can open the code we
provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 31：Temperature
Instrument\\Project\_31.2\_Temperature\_Instrument”**.

    //**********************************************************************************
    /*  
     * Filename    : Temperature Instrument
     * Description : LCD displays the temperature of thermistor.
     * Auther      : http//www.keyestudio.com
    */
    #include "lcd128_32_io.h"
    
    #define PIN_ANALOG_IN   36
    
    lcd lcd(21, 22); //Create lCD128 *32 pin，sda->21， scl->22
    
    void setup() {
      lcd.Init(); //initialize
      lcd.Clear();  //clear
    }
    char string[10];
    
    void loop() {
      int adcValue = analogRead(PIN_ANALOG_IN);                       //read ADC pin
      double voltage = (float)adcValue / 4095.0 * 3.3;                // calculate voltage
      double Rt = 10 * voltage / (3.3 - voltage);                     //calculate resistance value of thermistor
      double tempK = 1 / (1 / (273.15 + 25) + log(Rt / 10) / 3950.0); //calculate temperature (Kelvin)
      double tempC = tempK - 273.15;                                  //calculate temperature (Celsius)
      lcd.Cursor(0,0); //Set display position
      lcd.Display("Voltage:"); //Setting the display
      lcd.Cursor(0,8);
      lcd.DisplayNum(voltage);
      lcd.Cursor(0,11);
      lcd.Display("V");
      lcd.Cursor(2,0); 
      lcd.Display("tempC:");
      lcd.Cursor(2,8);
      lcd.DisplayNum(tempC);
      lcd.Cursor(2,11);
      lcd.Display("C");
      delay(200);
    }
    //**********************************************************************************


8. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that the LCD
128X32 DOT displays the voltage value of the thermistor and the
temperature value in the current environment.
