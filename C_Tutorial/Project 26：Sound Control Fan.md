# Project 26：Sound Control Fan

1. Introduction：

The sound sensor has a built-in capacitive electret microphone and power
amplifier which can be used to detect the sound intensity of the
environment. In this project, we use ESP32 to control the sound sensor
and the motor module to simulate a voice-controlled fan.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:1.59722in;height:0.77986in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.75972in;height:1.8625in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/43cc1e416eff4d721c840abb6ab94c72.png" style="width:0.9875in;height:0.7375in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>Sound Sensor*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/4dc1472ab8d2cf85fd7518646e10d0ee.png" style="width:1.16944in;height:0.5in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e9b89f352e8b03fd1d367f23dd0bddae.png" style="width:1.0625in;height:0.88681in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:0.99028in;height:0.52986in" /></td>
</tr>
<tr class="even">
<td>130 Motor Module*1</td>
<td>M-F Dupont Wires</td>
<td>USB Cable*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e07904c75497330fe5abe3b5c21d4d02.png" style="width:1.39653in;height:0.60278in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7d1024775eaf4d275ea7f3253ae2257c.jpeg" style="width:1.27778in;height:0.92222in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/a815c48437199c6ab79d74cd2d583de0.png" style="width:0.33472in;height:1.54236in" /></td>
</tr>
<tr class="even">
<td>Keyestudio bread board special power module*1</td>
<td>Battery Holder*1</td>
<td>No.5 battery (self-provided)*6</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/009965e315276ecf1144c22c54a93fd9.png" style="width:0.94375in;height:0.82986in" /></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Fan*1</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

3. Component knowledge：

![](/media/9271d5f7a7647d7a3c959e6c7b837b5b.png)

Sound sensor is usually used to detect the loudness of the sound in the
surrounding environment. Microcontrol board can collect its output
signal through the analog input interface.The S pin is an analog output,
which is the real-time output of the microphone voltage signal. The
sensor comes with a potentiometer so you can adjust the signal strength.
It also has two fixing holes so that the sensor can be installed on any
other equipment. You can use it to make some interactive works, such as
voice-operated switches.

4. Read the ADC value, DAC value and voltage value of the sound sensor：

We first use a simple code to read the ADC value, DAC value and voltage
value of the sound sensor and print them out. Please refer to the wiring
diagram below：

![](/media/87fb44c475d1f53aa5905cebfed55ea2.png)

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 26：Sound Control
Fan\\Project\_26.1\_Read\_Sound\_Sensor\_Analog\_Value”**.

    //**********************************************************************************
    /*  
     * Filename    : Read Sound Sensor Analog Value
     * Description : Basic usage of ADC
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_ANALOG_IN  36  //the pin of the Sound Sensor
    
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
sound sensor.When you clap your hands to the sensor, the ADC value，DAC
value and voltage value will change significantly.

![](/media/823f33b45e3ff5557d9d4a2da3a78875.png)

5. Wiring diagram of the intelligent fan：

Next, we officially entered the project. We used a sound sensor, a motor
module and a fan blade to simulate a voice-controlled fan. The wiring
diagram is as follows：

![](/media/5a08d512265e03c997bf81a9e2bfecbb.png)

(Note: Connect the wires and then install a small fan blade on the DC
motor. )

6. Project code：（Note：![](/media/c20911df19d11290cf099072fe250029.png)The threshold 600 in
the code can be reset itself as needed）

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 26：Sound Control
Fan\\Project\_26.2\_Sound\_Control\_Fan”**.

    //**********************************************************************************
    /*  
     * Filename    : Sound Control Fan
     * Description : Controlling the fan by Sound sensor.
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_ADC0   36  //the pin of the Sound sensor
    #define PIN_Motorla    15  // the Motor_IN+ pin of the motor
    #define PIN_Motorlb    2 // the Motor_IN- pin of the motor
    
    void setup() {
      pinMode(PIN_Motorla, OUTPUT);//set Motorla to OUTPUT
      pinMode(PIN_Motorlb, OUTPUT);//set Motorlb to OUTPUT
      pinMode(PIN_ADC0, INPUT);//set PIN_ADC2 to INPUT
    }
    
    void loop() {
      int adcVal = analogRead(PIN_ADC0); //read the ADC value of Sound sensor
      if (adcVal > 600) {
        digitalWrite(PIN_Motorla,HIGH); //rotate
        digitalWrite(PIN_Motorlb,LOW);
        delay(5000); //delay 5S
      }
      else
      {
        digitalWrite(PIN_Motorla,LOW); //stop rotating
        digitalWrite(PIN_Motorlb,LOW); 
      }
    }
    //**********************************************************************************


7. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, external power supply and power on. and then you will see
that clap your hands to the sound sensor, and when the sound intensity
exceeds a threshold, the small fan rotates; conversely, the small fan
doesn't rotate.
