# Project 05：Traffic Lights

1. Introduction：

Traffic lights are closely related to people's daily lives, which
generally show red, yellow, and green. Everyone should obey the traffic
rules, which can avoid many traffic accidents. In this project, we will
use ESP32 and some LEDs (red, green and yellow) to simulate the traffic
lights.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/c1a470aaea31f177097eacbcb17ee4c4.jpeg" style="width:1.21736in;height:0.59444in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/b57b4057770f0bcc43f037c0ab8e1c41.png" style="width:0.84375in;height:2.23125in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/afa6edd3ff90b027a6f43995a6fb15a2.png" style="width:0.28333in;height:1.20972in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/0c1b0f91b4e56bcbc235d06b48809ac9.png" style="width:0.27986in;height:1.22222in" /></td>
<td></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Bread board*1</td>
<td>Red LED*1</td>
<td>Yellow LED*1</td>
<td></td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/6c688493b558ed5f3e90e7dab38cbd93.png" style="width:0.26736in;height:1.16389in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.05903in;height:0.56667in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/098a2730d0b0a2a4b2079e0fc87fd38b.png" style="width:1.22639in;height:0.49236in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/c801a7baee258ff7f5f28ac6e9a7097b.png" style="width:0.66736in;height:0.64097in" /></td>
<td></td>
</tr>
<tr class="even">
<td>GreenLED*1</td>
<td>USB Cable*1</td>
<td>220Ω Resistor*3</td>
<td>Jumper Wires</td>
<td></td>
</tr>
</tbody>
</table>

3. Wiring diagram：

![](/media/a991f5cc6f8759eca3b9d01f95fe4854.png)

**Note:**

How to connect a LED

![](/media/42ff6f405dfa128593827de5aa03e94b.png)

How to identify the 220Ω Five-color ring resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

4. Project code：

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 05：Traffic
Lights\\Project\_05\_Traffic\_Lights”**.

    //**********************************************************************
    /*
     * Filename    : Traffic Lights
     * Description : Simulated traffic lights.
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_LED_RED   0   //define the red led pin
    #define PIN_LED_YELLOW   2   //define the yellow led pin
    #define PIN_LED_GREEN  15   //define the green led pin
    
    void setup() {
      pinMode(PIN_LED_RED, OUTPUT);
      pinMode(PIN_LED_YELLOW, OUTPUT);
      pinMode(PIN_LED_GREEN, OUTPUT);
    }
    
    void loop() {
       digitalWrite(PIN_LED_RED, HIGH);// turns on the red led
       delay(5000);// delays 5 seconds
       digitalWrite(PIN_LED_GREEN, LOW); // turns off the green led
       for(int i=0;i<3;i++)// flashes 3 times.
    {
       delay(500);// delays 0.5 second
       digitalWrite(PIN_LED_YELLOW, HIGH);// turns on the yellow led
       delay(500);// delays 0.5 second
       digitalWrite(PIN_LED_YELLOW, LOW);// turns off the yellow led
    } 
       delay(500);// delays 0.5 second
       digitalWrite(PIN_LED_GREEN, HIGH);// turns on the green led
       delay(5000);// delays 5 second
       digitalWrite(PIN_LED_RED, LOW);// turns off the red led
    }
    //*************************************************************************************


Before uploading Project Code to ESP32, please check the configuration
of Arduino IDE.

Click "**Tools**" to confirm the board type and port as shown below:

![](/media/8de3ae8603714382e29f89c118e95a23.png)

Click![](/media/b0d41283bf5ae66d2d5ab45db15331ba.png)to download the project code to ESP32.

![](/media/fe6fff7cbb098f691ee7b121edd25bc7.png)

**Note:** If uploading the code fails, you can press the Boot button on
ESP32 after click![](/media/d09c4a31563f04a42d451e7bc1a5fb8a.png), and release the Boot
button![](/media/dc77bfcf5851c8f43aab6cbe7cec7920.png) after the percentage of uploading progress
appears, as shown below:

![](/media/157ee2e7687559d9812d24edec758150.png)

The Project code is uploaded successfully！

![](/media/d1fc96fdeadfde93bf4dd57ec7f1caab.png)

5. Project result：

After the project code was uploaded successfully, power up with a USB
cable and you'll see are below:

① First, the green light will be on for five seconds and then off; 

② Next, the yellow light blinks three times and then goes off;

③ Then, the red light goes on for five seconds and then goes off;

④ Repeat steps 1 to 3 above.
