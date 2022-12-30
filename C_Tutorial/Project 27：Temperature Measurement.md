# Project 27：Temperature Measurement

1. Introduction：

LM35 is a common used and easy-to-use temperature sensor. It doesn't
require any other hardware and you only need an analog port. The
difficulty lies in compiling the code and converting the analog values
to Celsius temperature. In this project, we used a temperature sensor
and 3 LEDs to make a temperature tester. When the temperature sensor
touches different temperature objects, the LEDs will show different
colors.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:1.59722in;height:0.77986in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.73542in;height:1.80347in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/0fded1cfe95575d0fa4aa03839d8e30d.png" style="width:1.41458in;height:1.04514in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:0.99028in;height:0.52986in" /></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>LM35*1</td>
<td>USB Cable*1</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/098a2730d0b0a2a4b2079e0fc87fd38b.png" style="width:1.09792in;height:0.44097in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/afa6edd3ff90b027a6f43995a6fb15a2.png" style="width:0.28333in;height:1.20972in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/0c1b0f91b4e56bcbc235d06b48809ac9.png" style="width:0.27986in;height:1.22222in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/6c688493b558ed5f3e90e7dab38cbd93.png" style="width:0.26736in;height:1.16389in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/849dad1bcb5c3177310976501fbc96c9.png" style="width:1.14583in;height:0.96806in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e9a8d050105397bb183512fb4ffdd2f6.png" style="width:1.09167in;height:1.08472in" /></td>
</tr>
<tr class="even">
<td>220Ω Resistor*3</td>
<td>Red LED*1</td>
<td>Yellow LED*1</td>
<td>Green LED*1</td>
<td>M-F Dupont Wires</td>
<td>Jumper Wires</td>
</tr>
</tbody>
</table>

3. Component knowledge：

![](/media/0fded1cfe95575d0fa4aa03839d8e30d.png)

**Working principle of LM35 temperature sensor:** LM35 temperature
sensor is a widely used temperature sensor with a variety of package
types. At room temperature, it can achieve the accuracy of 1/4°C without
additional calibration processing. LM35 temperature sensor can produce
different voltage according to different temperatures, when the
temperature is 0 ℃, it output 0V; If increasing 1 ℃, the output voltage
will increase 10mv. The output temperature is 0℃ to 100℃, the conversion
formula is as follows：

![](/media/0dfa07fa69f2a98658a3822c2da93bf7.jpeg)

4. Read the temperature value of LM35：

We first use a simple code to read the value of the temperature sensor
and printing them out, wiring diagram is shown below：

![](/media/041471b9fabd75ef9dc3951598e342f8.png)

LM35 output is given to analog pin GPIO36 of the ESP32, this analog
voltage is converted to its digital form and processed to get the
temperature reading.

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 27：Temperature
Measurement\\Project\_27.1\_Read\_LM35\_Temperature\_Value”**.

    //**********************************************************************************
    /*  
     * Filename    : Read LM35 Temperature Value
     * Description : ADC value is converted to LM35 temperature value
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_ANALOG_IN  36  //the pin of the Temperature Sensor
    
    void setup() {
      Serial.begin(115200);
    }
    
    //In loop()，the analogRead() function is used to obtain the ADC value, 
    //and then the map() function is used to convert the value into an 8-bit precision DAC value. 
    //Calculate the measured voltage value,Celsius and Fahrenheit valuesthrough the formula, 
    //and print these data through the serial port monitor.
    void loop() {
      int adcVal = analogRead(PIN_ANALOG_IN);
      int dacVal = map(adcVal, 0, 4095, 0, 255);
      double voltage = adcVal / 4095.0 * 3.3;
      float temperatureC = (voltage * 1000.0) / 10.0 ;
      float temperatureF = (temperatureC * 1.8) + 32.0;
      Serial.print("ADC Value: " + String(adcVal));
      Serial.print("--DAC Value: " + String(dacVal));
      Serial.print("--Voltage Value: " + String(voltage) + "V");
      Serial.print("--temperatureC: " + String(temperatureC) + "℃");
      Serial.println("--temperatureF: " + String(temperatureF) + "F");
      delay(200);
    }
    //**********************************************************************************


Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable, open the serial monitor and set
the baud rate to 115200. You will see that the serial port monitor
window will print out the temperature values read by the LM35
temperature sensor. Hold the LM35 element by hand, the temperature value
read by the LM35 temperature sensor will change.

![](/media/c58d1c70e1a3ad105ff7c77c4092e5f1.png)

5. Wiring** **diagram of the temperature measurement：

Now we use a LM35 temperature sensor and three LED lights to do a
temperature test. When the LM35 temperature sensor senses different
temperatures, different LED lights will light up. Follow the diagram
below for wiring.

![](/media/831ebf50a9b59c744cbd93ac2170d64b.png)

6. Project code：

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 27：Temperature
Measurement\\Project\_27.2\_Temperature\_Measurement”**.

(Note: The temperatureC threshold in the code can be reset itself as
required.)

    //**********************************************************************************
    /*  
     * Filename    : Temperature Measurement
     * Description : Different leds light up when the LM35 senses different temperatures
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_ADC0       36      //the pin of the LM35 Sensor
    #define PIN_GREENLED   4      //the pin of the Green led
    #define PIN_YELLOWLED  2      //the pin of the Yellow led
    #define PIN_REDLED     15      //the pin of the Red led
    void setup() {
      Serial.begin(115200);
      pinMode(PIN_GREENLED, OUTPUT); //set PIN_GREENLED to OUTPUT
      pinMode(PIN_YELLOWLED, OUTPUT);//set PIN_YELLOWLED to OUTPUT
      pinMode(PIN_REDLED, OUTPUT);//set PIN_REDLED to OUTPUT
      pinMode(PIN_ADC0, INPUT);//set PIN_ADC0 to INPUT
    }
    
    void loop() {
      int adcVal = analogRead(PIN_ADC0);
      double voltage = adcVal / 4095.0 * 3.3;
      float temperatureC = (voltage * 1000.0) / 10.0 ;
      float temperatureF = (temperatureC * 1.8) + 32.0;
      Serial.print("ADC Value: " + String(adcVal));
      Serial.print("---Voltage Value: " + String(voltage) + "V");
      Serial.print("---temperatureC: " + String(temperatureC) + "℃");
      Serial.println("---temperatureF: " + String(temperatureF) + "F");
      if (temperatureC >= 25) {
        delay(100);
        digitalWrite(PIN_GREENLED, LOW);
        digitalWrite(PIN_YELLOWLED, LOW);
        digitalWrite(PIN_REDLED, HIGH);
      }
      else if (temperatureC >= 20 && temperatureC < 25) {
        digitalWrite(PIN_GREENLED, LOW);
        digitalWrite(PIN_YELLOWLED, HIGH);
        digitalWrite(PIN_REDLED, LOW);
      }
      else {
        digitalWrite(PIN_GREENLED, HIGH);
        digitalWrite(PIN_YELLOWLED, LOW);
        digitalWrite(PIN_REDLED, LOW);
      }
    
      delay(500);
    }
    //**********************************************************************************


7. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that the
monitor displays the temperature values read by the LM35 temperature
sensor. When the LM35 temperature sensor senses different temperatures,
different LEDs will light up.
