# Project 24：Night Lamp

1.Introduction：

Sensors or components are ubiquitous in our daily life. For example,
some public street lamps will automatically turn on at night and turn
off during the day. Why? In fact, this make use of a photosensitive
element that senses the intensity of external ambient light. When the
outdoor brightness decreases at night, the street lights will turn on
automatically; In the daytime, the street lights will automatically turn
off. the principle of which is very simple, In this Project, we use
ESP32 to control a LED to achieve the effect of the street light.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/d8beaf7391033a5f6ba4600791f8c348.jpeg" style="width:1.38681in;height:0.67708in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.6in;height:1.47083in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/ef77f5a64c382157fc2dea21ec373fef.png" style="width:0.29514in;height:1.25903in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/b395b1cd2678f87b3a34dec15659efbc.png" style="width:0.22431in;height:1.00556in" /></td>
<td></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>Red LED*1</td>
<td>10KΩResistor*1</td>
<td></td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/9e553e75b6f976f33438171eb2f2e775.png" style="width:0.19097in;height:1.26597in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/845d05a6108b1662b828610ba9dcb788.png" style="width:0.25833in;height:1.13681in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e9a8d050105397bb183512fb4ffdd2f6.png" style="width:0.77222in;height:0.77986in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:0.99028in;height:0.52986in" /></td>
<td></td>
</tr>
<tr class="even">
<td>Photoresistor*1</td>
<td>220ΩResistor*1</td>
<td>Jumper Wires</td>
<td>USB Cable*1</td>
<td></td>
</tr>
</tbody>
</table>

3. Component knowledge：

![](/media/9e553e75b6f976f33438171eb2f2e775.png)

**Photoresistor :** It is a kind of photosensitive resistance, its
principle is that the photoresistor surface receives brightness (light)
to reduce the resistance, the resistance value will change with the
detected intensity of the ambient light . With this characteristic, we
can use the photosensitive resistance to detect the light intensity.
Photosensitive resistance and its electronic symbol are as follows：

![](/media/7d575da675a2f6cb511d28b801e2abaa.png)

The following circuit is used to detect changes in resistance values of
photoresistors：

![](/media/5a7f7e641eb78007760a94151c1d80a5.png)

In the circuit above, when the resistance of the photoresistor changes
due to the change of light intensity, the voltage between the
photoresistor and resistance R2 will also change.  Thus, the intensity
of light can be obtained by measuring this voltage.

4. Read the ADC value, DAC value and voltage value of the photoresistor：

We first use a simple code to read the ADC value, DAC value and voltage
value of the photoresistor and print them out. Please refer to the
following wiring diagram：

![](/media/b762098c798beb08e4d433137c317dc7.png)

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\****2. C\_Tutorial\\2. Projects\\Project 24：Night
Lamp\\Project\_24.1\_Read\_Photosensitive\_Analog\_Value”**.

    //**********************************************************************************
    /*  
     * Filename    : Read Photosensitive Analog Value
     * Description : Basic usage of ADC
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_ANALOG_IN  36  //the pin of the photosensitive sensor
    
    void setup() {
      Serial.begin(115200);
    }
    
    //In loop()，the analogRead() function is used to obtain the ADC value, 
    //and then the map() function is used to convert the value into an 8-bit precision DAC value. 
    //The input and output voltage are calculated according to the previous formula, 
    //and the information is finally printed out.
    void loop() {
      int adcVal = analogRead(PIN_ANALOG_IN);
      int dacVal = map(adcVal, 0, 4095, 0, 255);
      double voltage = adcVal / 4095.0 * 3.3;
      Serial.printf("ADC Val: %d, \t DAC Val: %d, \t Voltage: %.2fV\n", adcVal, dacVal, voltage);
      delay(200);
    }
    //**********************************************************************************


Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable, open the serial monitor and set
the baud rate to 115200. You will see that the serial port monitor
window will print out the ADC value、DAC value and voltage value of the
photoresistor. When the light intensity around the photoresistor is
gradually reduced, the ADC value, DAC value and voltage value will
gradually increase. On the contrary, the ADC value, DAC value and
voltage value decreases gradually.

![](/media/36d48be9ba9a78c2e1ce41fb0c35cd46.png)

5. Wiring diagram of the light-controlled lamp：

We made a small dimming lamp in the front, now we will make a light
controlled lamp. The principle is the same, that is, the ESP32 takes the
ADC value of the sensor, and then adjusts the brightness of the LED.

![](/media/77a0c534501f51e7fe7aa221e4db71d9.png)

6. Project code：

You can open the code we provide:

The code used in this project is saved in folder**“2. Windows
System****\\****2. C\_Tutorial\\2. Projects\\Project 24：Night
Lamp\\Project\_24.2\_Night\_Lamp”**.

    //**********************************************************************************
    /*  
     * Filename    : Night Lamp
     * Description : Controlling the brightness of LED by photosensitive sensor.
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_ANALOG_IN    36  // the pin of the photosensitive sensor
    #define PIN_LED     15  // the pin of the LED
    #define CHAN            0
    #define LIGHT_MIN       372
    #define LIGHT_MAX       2048
    void setup() {
      ledcSetup(CHAN, 1000, 12);
      ledcAttachPin(PIN_LED, CHAN);
    }
    
    void loop() {
      int adcVal = analogRead(PIN_ANALOG_IN); //read adc
      int pwmVal = map(constrain(adcVal, LIGHT_MIN, LIGHT_MAX), LIGHT_MIN, LIGHT_MAX, 0, 4095);  // adcVal re-map to pwmVal
      ledcWrite(CHAN, pwmVal);    // set the pulse width.
      delay(10);
    }
    //**********************************************************************************


7. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see thatwhen the
intensity of light around the photoresistor is reduced, the LED will be
bright, on the contraty, the LED will be dim.
