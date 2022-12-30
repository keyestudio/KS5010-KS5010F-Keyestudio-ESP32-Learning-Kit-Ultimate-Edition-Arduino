# Project 22：Dimming Light

1. Introduction：

A potentiometer is a three-terminal resistor with sliding or rotating
contacts that forms an adjustable voltage divider. It works by changing
the position of the sliding contacts across a uniform resistance. In the
potentiometer, the entire input voltage is applied across the whole
length of the resistor, and the output voltage is the voltage drop
between the fixed and sliding contact.

In this project, we will learn how to use ESP32 to read the values of
the potentiometer, and make a dimming lamp with LED.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:1.74861in;height:0.85347in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.64028in;height:1.56944in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/03ab81e8b4f09287d2781ef0fd297f85.png" style="width:0.70556in;height:1.08125in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/a3acf081c77644a721e572c18772b36e.png" style="width:0.23819in;height:1.01667in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>Potentiometer*1</td>
<td>Red LED*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/845d05a6108b1662b828610ba9dcb788.png" style="width:0.25833in;height:1.13681in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e9a8d050105397bb183512fb4ffdd2f6.png" style="width:0.77222in;height:0.77986in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.05903in;height:0.56667in" /></td>
<td></td>
</tr>
<tr class="even">
<td>220ΩResistor*1</td>
<td>Jumper Wires</td>
<td>USB Cable*1</td>
<td></td>
</tr>
</tbody>
</table>

3. Component knowledge：

![](/media/03ab81e8b4f09287d2781ef0fd297f85.png)

**Adjustable potentiometer:** It is a kind of resistor and an analog
electronic component, which has two states of 0 and 1(high level and low
level). The analog quantity is different, its data state presents a
linear state such as 1 \~ 1024。

**ADC :** An ADC is an electronic integrated circuit used to convert
analog signals such as voltages to digital or binary form consisting of
1s and 0s. The range of our ADC on ESP32 is 12 bits, that means the
resolution is 2^12=4096, and it represents a range (at 3.3V) will be
divided equally to 4096 parts. The rage of analog values corresponds to
ADC values. So the more bits the ADC has, the denser the partition of
analog will be and the greater the precision of the resulting
conversion.

![](/media/f6c45550f4adf8373d7f1d01daec2c64.png)

Subsection 1: the analog in rang of 0V---3.3/4095 V corresponds to
digital 0;

Subsection 2: the analog in rang of 3.3/4095 V---2\*3.3 /4095V
corresponds to digital 1;

…

The following analog will be divided accordingly.

The conversion formula is as follows:

**DAC：**The reversing of this process requires a DAC, Digital-to-Analog
Converter. The digital I/O port can output high level and low level (0
or 1), but cannot output an intermediate voltage value. This is where a
DAC is useful. ESP32 has two DAC output pins with 8-bit accuracy, GPIO25
and GPIO26, which can divide VCC

(here is 3.3V) into 2^8=256 parts. For example, when the digital
quantity is 1, the output voltage value is 3.3/256 \*1 V, and when the
digital quantity is 128, the output voltage value is 3.3/256
\*128=1.65V, the higher the accuracy of DAC, the higher the accuracy of
output voltage value will be.

The conversion formula is as follows:

**ADC on ESP32：**

ESP32 has 16 pins can be used to measure analog signals. GPIO pin
sequence number and analog pin definition are shown in the following
table：

<table>
<tbody>
<tr class="odd">
<td><strong>ADC number in ESP32</strong></td>
<td><strong>ESP32 GPIO number</strong></td>
</tr>
<tr class="even">
<td><strong>ADC0</strong></td>
<td><strong>GPIO 36</strong></td>
</tr>
<tr class="odd">
<td><strong>ADC3</strong></td>
<td><strong>GPIO 39</strong></td>
</tr>
<tr class="even">
<td><strong>ADC4</strong></td>
<td><strong>GPIO 32</strong></td>
</tr>
<tr class="odd">
<td><strong>ADC5</strong></td>
<td><strong>GPIO33</strong></td>
</tr>
<tr class="even">
<td><strong>ADC6</strong></td>
<td><strong>GPIO34</strong></td>
</tr>
<tr class="odd">
<td><strong>ADC7</strong></td>
<td><strong>GPIO 35</strong></td>
</tr>
<tr class="even">
<td><strong>ADC10</strong></td>
<td><strong>GPIO 4</strong></td>
</tr>
<tr class="odd">
<td><strong>ADC11</strong></td>
<td><strong>GPIO0</strong></td>
</tr>
<tr class="even">
<td><strong>ADC12</strong></td>
<td><strong>GPIO2</strong></td>
</tr>
<tr class="odd">
<td><strong>ADC13</strong></td>
<td><strong>GPIO15</strong></td>
</tr>
<tr class="even">
<td><strong>ADC14</strong></td>
<td><strong>GPIO13</strong></td>
</tr>
<tr class="odd">
<td><strong>ADC15</strong></td>
<td><strong>GPIO 12</strong></td>
</tr>
<tr class="even">
<td><strong>ADC16</strong></td>
<td><strong>GPIO 14</strong></td>
</tr>
<tr class="odd">
<td><strong>ADC17</strong></td>
<td><strong>GPIO27</strong></td>
</tr>
<tr class="even">
<td><strong>ADC18</strong></td>
<td><strong>GPIO25</strong></td>
</tr>
<tr class="odd">
<td><strong>ADC19</strong></td>
<td><strong>GPIO26</strong></td>
</tr>
</tbody>
</table>

**DAC on ESP32：**

ESP32 has two 8-bit digital analog converters to be connected to GPIO25
and GPIO26 pins, respectively, and it is immutable. As shown in the
following table：

<table>
<tbody>
<tr class="odd">
<td><strong>Simulate pin number</strong></td>
<td><strong>GPIO number</strong></td>
</tr>
<tr class="even">
<td><strong>DAC1</strong></td>
<td><strong>GPIO25</strong></td>
</tr>
<tr class="odd">
<td><strong>DAC2</strong></td>
<td><strong>GPIO26</strong></td>
</tr>
</tbody>
</table>

The DAC pin number is already defined in ESP32's code base; for example,
you can replace GPIO25 with DAC1 in the code.

4.  **Read the ADC value, DAC value and voltage value of the
potentiometer：**

We connect the potentiometer to the analog IO port of ESP32 to read the
ADC value, DAC value and voltage value of the potentiometer, please
refer to the wiring diagram below：

![](/media/0cda3256a0930404abc097ec8ffa3013.png)

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 22：Dimming
Light\\Project\_22.1\_Read\_Potentiometer\_Analog\_Value”**.

    //**********************************************************************************
    /*  
     * Filename    : Read Potentiometer Analog Value
     * Description : Basic usage of ADC，DAC and Voltage
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_ANALOG_IN  36  //the pin of the Potentiometer
    
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
window will print out the ADC value, DAC value and voltage value of the
potentiometer. When turning the potentiometer handle, the ADC value, DAC
value and voltage value will change. As shown below:

![](/media/36d48be9ba9a78c2e1ce41fb0c35cd46.png)

5. Wiring diagram of the dimming lamp：

In the previous step, we read the ADC value, DAC value and voltage value
of the potentiometer. Now we need to convert the ADC value of the
potentiometer into the brightness of the LED to make a lamp that can
adjust the brightness.The wiring diagram is as follows:

![](/media/3396bd77169711de6e15da73f14c8afb.png)

6. Project code：

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 22：Dimming
Light\\Project\_22.2\_Dimming\_Light”**.

    //**********************************************************************************
    /*  
     * Filename    : Dimming Light
     * Description : Controlling the brightness of LED by potentiometer.
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_ANALOG_IN    36  //the pin of the potentiometer
    #define PIN_LED     15  // the pin of the LED
    #define CHAN            0
    void setup() {
      ledcSetup(CHAN, 1000, 12);
      ledcAttachPin(PIN_LED, CHAN);
    }
    
    void loop() {
      int adcVal = analogRead(PIN_ANALOG_IN); //read adc
      int pwmVal = adcVal;        // adcVal re-map to pwmVal
      ledcWrite(CHAN, pwmVal);    // set the pulse width.
      delay(10);
    }
    //**********************************************************************************


7. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that turn the
potentiometer handle and the brightness of the LED will change
accordingly.

![](/media/eca30dead3f4923afa0dcb0306db2319.jpeg)
