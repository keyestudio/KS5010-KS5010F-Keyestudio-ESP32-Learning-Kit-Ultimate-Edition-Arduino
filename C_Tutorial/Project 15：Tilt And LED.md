# Project 15：Tilt and LED

1. Introduction：

The ancients without electronic clock, so the hourglass are invented
to measure time. The hourglass has a large capacity on both sides,
and which is filled with fine sand on one side. What’s more, there
is a small channel in the middle, which can make the hourglass stand
upright , the side with fine sand is on the top. due to the effect
of gravity,the fine sand will flow down through the channel to the
other side of the hourglass. When the sand reaches the bottom, turn
it upside down and record the number of times it has gone through
the hourglass, therefore, the next day we can know the approximate
time of the day by it. In this project, we will use ESP32 to control
the tilt switch and LED lights to simulate an hourglass and make an
electronic hourglass.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:1.59236in;height:0.77778in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/36f15610f430e5d5138f4e4fb721c40f.png" style="width:1.27292in;height:0.71667in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/ef77f5a64c382157fc2dea21ec373fef.png" style="width:0.29514in;height:1.25903in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/da8a2a9d15baf7280966f3fdbb025a8c.png" style="width:0.26042in;height:1.16667in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Tilt Switch*1</td>
<td>Red LED*4</td>
<td>10KΩ Resistor*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.59028in;height:1.44583in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/845d05a6108b1662b828610ba9dcb788.png" style="width:0.25833in;height:1.13681in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.05903in;height:0.56667in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e9a8d050105397bb183512fb4ffdd2f6.png" style="width:0.8375in;height:0.83194in" /></td>
</tr>
<tr class="even">
<td>Breadboard*1</td>
<td>220Ω Resistor*4</td>
<td>USB Cable*1</td>
<td>Jumper Wires</td>
</tr>
</tbody>
</table>

3. Component knowledge：

![](/media/8c40739f8e05f753f145420b421a0f47.png)

Tilt switch is also called digital switch. Inside is a metal ball that
can roll. The principle of rolling the metal ball to contact with the
conductive plate at the bottom, which is used to control the on and off
of the circuit. When it is a rolling ball tilt sensing switch with
single directional trigger, the tilt sensor is tilted toward the trigger
end (two gold-plated pin ends), the tilt switch is in a closed circuit
and the voltage at the analog port is about 5V(binary number is 1023),
In this way, the LED will light up. When the tilting switch is in
horizontal position or tilting to the other end, the tilting switch is
in open state the voltage of the analog port is about 0V (binary number
is 0), the LED will turn off. In the program, we judge the state of the
switch based on whether the voltage value of the analog port is greater
than 2.5V (binary number is 512).

The internal structure of the tilt switch is used here to illustrate how
it works, as shown below:

![](/media/bf8b10ad248ac939ac4ef96d02ed87c7.png)

4. Wiring Diagram：

![](/media/a46c0b8be898ba596308ce56993c26ba.png)

**Note:**

How to connect the LED

![](/media/f70404aa49540fd7aecae944c7c01f83.jpeg)

How to identify the 220Ω 5-band resistor and 10KΩ 5-band resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

![](/media/246cf3885dc837c458a28123885c9f7b.png)

5. Project code：

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 15：Tilt And
LED\\Project\_15\_Tilt\_And\_LED****”**.

    //**********************************************************************
    /* 
     * Filename    : Tilt And LED
     * Description : Tilt switches and four leds to simulate an hourglass.
     * Auther      : http//www.keyestudio.com
    */
    #define SWITCH_PIN  15  // the tilt switch is connected to Pin15
    byte switch_state = 0;
    void setup()
    {
         for(int i=16;i<20;i++)
      {
            pinMode(i, OUTPUT);
      } 
        pinMode(SWITCH_PIN, INPUT);
     for(int i=16;i<20;i++)
      {
        digitalWrite(i,0);
      } 
      Serial.begin(9600);
    }
    void loop()
    {
    switch_state = digitalRead(SWITCH_PIN); 
    Serial.println(switch_state);
     if (switch_state == 0) 
     {
     for(int i=16;i<20;i++)
      {
        digitalWrite(i,1);
        delay(500);
      } 
      }
       if (switch_state == 1) 
     {
       for(int i=19;i>15;i--)
       {
        digitalWrite(i,0);
        delay(500);
       }
      }
    }
    //**********************************************************************************


6. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that when you
tilt the breadboard to an angle, the LEDs will light up one by one. When
you turn the breadboard to the original angle, the LEDs will turn off
one by one. Like the hourglass, the sand will leak out over time.
