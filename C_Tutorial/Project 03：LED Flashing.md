# Project 03：LED Flashing 

1. Introduction：

In this project, we will show you the LED flashing effect .We use the
ESP32's digital pin to turn on the LED and make it flashing.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:2.17847in;height:1.0625in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.95208in;height:2.33472in" /></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7eb361d680dfa351f07f8527aeb37abd.png" style="width:0.275in;height:1.17361in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/098a2730d0b0a2a4b2079e0fc87fd38b.png" style="width:1.22639in;height:0.49236in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/c801a7baee258ff7f5f28ac6e9a7097b.png" style="width:0.66736in;height:0.64097in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.05903in;height:0.56667in" /></td>
</tr>
<tr class="even">
<td>Red LED*1</td>
<td>220Ω Resistor*1</td>
<td>Jumper Wire*2</td>
<td>USB Cable*1</td>
</tr>
</tbody>
</table>

3. Wiring diagram：

First, disconnect all power from the ESP32. Then build the circuit
according to the wiring diagram. After the circuit is built and verified
correct, connect the ESP32 to your computer using a USB cable.

**Note:** Avoid any possible short circuits (especially connecting 3.3V
and GND)\!

**WARNING:** A short circuit can cause high current in your circuit,
create excessive component heat and cause permanent damage to your
hardware\!

![](/media/0735997593c8858ad6441d8e9867206f.png)

**Note:**

How to connect a LED

![](/media/42ff6f405dfa128593827de5aa03e94b.png)

How to identify the 220Ω Five-color ring resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

**4. Project code：**

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 03：LED
Flashing\\Project\_03\_LED\_Flashing”**.

    //**********************************************************************
    /*
     * Filename    : External LED flashing
     * Description : Make an led blinking.
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_LED   15   //define the led pin
    
    // the setup function runs once when you press reset or power the board
    void setup() {
      // initialize digital pin LED as an output.
      pinMode(PIN_LED, OUTPUT);
    }
    
    // the loop function runs over and over again forever
    void loop() {
      digitalWrite(PIN_LED, HIGH);   // turn the LED on (HIGH is the voltage level)
      delay(500);                       // wait for 0.5s
      digitalWrite(PIN_LED, LOW);    // turn the LED off by making the voltage LOW
      delay(500);                       // wait for 0.5s
    }
    //*************************************************************************************


Before uploading Project Code to ESP32, please check the configuration
of Arduino IDE.

Click "**Tools**" to confirm the board type and port as shown below:

![](/media/03b4119e3a33069092df044bdaec21b3.png)

Click![](/media/b0d41283bf5ae66d2d5ab45db15331ba.png)to download the project code to ESP32.

![](/media/8ed303e3951bf68a2f3e281b21e94447.png)

**Note:** If uploading the code fails, you can press the Boot button on
ESP32 after click![](/media/d09c4a31563f04a42d451e7bc1a5fb8a.png), and release the Boot
button![](/media/dc77bfcf5851c8f43aab6cbe7cec7920.png) after the percentage of uploading progress
appears, as shown below:

![](/media/157ee2e7687559d9812d24edec758150.png)

The Project code is uploaded successfully！

![](/media/3577202bbda59bdbe7ddf52ad06bb450.png)

5. Project result：

After the project code was uploaded successfully, power up with a USB
cable and the LED start flashing.

![](/media/2dcc6a55b77b4175b5175f717eb196c3.png)
