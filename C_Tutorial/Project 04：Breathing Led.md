# Project 04: Breathing Led

1. Introduction：

In previous studies, we know that LEDs have on/off state, so how to
enter the intermediate state? How to output an intermediate state to
make the LED half bright? That's what we're going to learn.

Breathing light, that is, LED is turned from off to on gradually, and
gradually from on to off, just like "breathing". So, how to control the
brightness of a LED? We will use ESP32’s PWM to achieve this target.

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

3. Component knowledge：

![](/media/6549bdbfd4e7b6b2b341012105d655e8.png)

**Analog & Digital**

An Analog Signal is a continuous signal in both time and value. On the
contrary, a Digital Signal or discrete time signal is a time series
consisting of a sequence of quantities. Most signals in life are analog
signals. A familiar example of an Analog Signal would be how the
temperature throughout the day is continuously changing and could not
suddenly change instantaneously from 0℃ to 10℃. However, Digital Signals
can instantaneously change in value. This change is expressed in numbers
as 1 and 0 (the basis of binary code). Their differences can more easily
be seen when compared when graphed as below.

![](/media/4bdf6127e563b453a1fd8953b4ebb277.png)

In practical application, we often use binary as the digital signal,
that is a series of 0’s and 1’s. Since a binary signal only has two
values (0 or 1), it has great stability and reliability. Lastly, both
analog and digital signals can be converted into the other.

**PWM：**

PWM, Pulse-Width Modulation, is a very effective method for using
digital signals to control analog circuits. Common processors cannot
directly output analog signals. PWM technology makes it very convenient
to achieve this conversion (translation of digital to analog signals).

PWM technology uses digital pins to send certain frequencies of square
waves, that is, the output of high levels and low levels, which
alternately last for a while. The total time for each set of high levels
and low levels is generally fixed, which is called the period (Note: the
reciprocal of the period is frequency). The time of high level outputs
are generally called “pulse width”, and the duty cycle is the percentage
of the ratio of pulse duration, or pulse width (PW) to the total period
(T) of the waveform.

The longer the output of high levels last, the longer the duty cycle and
the higher the corresponding voltage in the analog signal will be. The
following figures show how the analog signal voltages vary between
0V-3V3 (high level is 3V3) corresponding to the pulse width 0%-100%:

![](/media/a439e1bd8a4578b43b7188c821d58594.jpeg)

The longer the PWM duty cycle is, the higher the output power will be.
Now that we understand this relationship, we can use PWM to control the
brightness of an LED or the speed of DC motor and so on. It is evident
from the above that PWM is not real analog, and the effective value of
the voltage is equivalent to the corresponding analog. so, we can
control the output power of the LED and other output modules to achieve
different effects.

**ESP32 and PWM:**

On ESP32, the LEDC(PWM) controller has 16 separate channels, each of
which can independently control frequency, duty cycle, and even
accuracy. Unlike traditional PWM pins, the PWM output pins of ESP32 are
configurable, with one or more PWM output pins per channel. The
relationship between the maximum

frequency and bit precision is shown in the following formula, where the
maximum value of bit is 31.

![](/media/f79af745d3c726ee5ca07932d2ca6d5e.png)

For example, generate a PWM with an 8-bit precision (2<sup>8</sup>=256.
Values range from 0 to 255) with a maximum frequency of 80,000,000/255 =
312,500Hz.）

4. Wiring diagram：

![](/media/0735997593c8858ad6441d8e9867206f.png)

**Note:**

How to connect a LED

![](/media/42ff6f405dfa128593827de5aa03e94b.png)

How to identify the 220Ω Five-color ring resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

5. Project code：

The design of this project makes the GP15 output PWM, and the pulse
width gradually increases from 0% to 100%, and then gradually decreases
from 100% to 0%.

You can open the code we provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 04：Breathing
Led\\Project\_04\_Breathing\_Led”**.

    //**********************************************************************
    /*
     * Filename    : Breathing Led
     * Description : Make led light fade in and out, just like breathing.
     * Auther      : http//www.keyestudio.com
    */
    #define PIN_LED   15   //define the led pin
    #define CHN       0   //define the pwm channel
    #define FRQ       1000  //define the pwm frequency
    #define PWM_BIT   8     //define the pwm precision
    void setup() {
      ledcSetup(CHN, FRQ, PWM_BIT); //setup pwm channel
      ledcAttachPin(PIN_LED, CHN);  //attach the led pin to pwm channel
    }
    
    void loop() {
      for (int i = 0; i < 255; i++) { //make light fade in
        ledcWrite(CHN, i);
        delay(10);
      }
      for (int i = 255; i > -1; i--) {  //make light fade out
        ledcWrite(CHN, i);
        delay(10);
      }
    }
    //*************************************************************************************


Before uploading Project Code to ESP32, please check the configuration
of Arduino IDE.

Click "**Tools**" to confirm the board type and port as shown below:

![](/media/ab8788f7c86b4103f086dc848618fadc.png)

Click![](/media/b0d41283bf5ae66d2d5ab45db15331ba.png)to download the project code to ESP32.

![](/media/a5502f90a619fb10a29492d47b8baec3.png)

**Note:** If uploading the code fails, you can press the Boot button on
ESP32 after click![](/media/d09c4a31563f04a42d451e7bc1a5fb8a.png), and release the Boot
button![](/media/dc77bfcf5851c8f43aab6cbe7cec7920.png) after the percentage of uploading progress
appears, as shown below:

![](/media/157ee2e7687559d9812d24edec758150.png)

The Project code is uploaded successfully\!

![](/media/96dba75dae8bbd81495ed3dd88b179a4.png)

6. Project result：

After the project code was uploaded successfully, power up with a USB
cable and the LED is turned from ON to OFF and then back from OFF to ON
gradually like breathing.

![](/media/3673c95868f245ee28365de8e51d2ced.png)
