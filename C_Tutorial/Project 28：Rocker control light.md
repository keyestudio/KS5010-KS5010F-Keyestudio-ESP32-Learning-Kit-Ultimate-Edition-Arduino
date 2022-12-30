# Project 28：Rocker control light

1. Introduction：

The rocker module is a component with two analog inputs and one digital
input. It is widely used in areas such as game operation、robot control
and drone control. In this project, we use ESP32 and a joystick module
to control RGB, so that you can have a deeper understanding of the
principle and operation of the joystick module in practice. 

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:1.59722in;height:0.77986in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.75972in;height:1.8625in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/d087b123748cbfb8ed9f517150db71c5.png" style="width:1.71042in;height:0.95139in" /></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>Rocker Module*1</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/af749ecbde89c728a8c63e6527781cac.png" style="width:0.16806in;height:0.93194in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/098a2730d0b0a2a4b2079e0fc87fd38b.png" style="width:1.22639in;height:0.49236in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/c801a7baee258ff7f5f28ac6e9a7097b.png" style="width:0.92778in;height:0.89167in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.14167in;height:0.61111in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/f1aed48e2c02214415853ad2358f3744.png" style="width:1.21875in;height:1.02986in" /></td>
</tr>
<tr class="even">
<td>RGB LED*1</td>
<td>220ΩResistor*3</td>
<td>Jumper Wires</td>
<td>USB Cable*1</td>
<td>M-F Dupont Wires</td>
</tr>
</tbody>
</table>

3. Component knowledge：

![](/media/d087b123748cbfb8ed9f517150db71c5.png)

**Rocker module:** It mainly uses PS2 joystick components. In fact, the
joystick module has 3 signal terminal pins, which simulate a
three-dimensional space. The pins of the joystick module are GND, VCC,
and signal terminals (B, X, Y). The signal terminals X and Y simulate
the X-axis and Y-axis of the space. When controlling, the X and Y signal
terminals of the module are connected to the analog port of the
microcontroller. The signal terminal B simulates the Z axis of the
space, it is generally connected to the digital port and used as a
button.

VCC is connected to the microcontroller power output VCC (3.3V or 5V),
GND is connected to the microcontroller GND, the voltage in the original
state is about 1.65V or 2.5V. In the X-axis direction, when moving in
the direction of the arrow, the voltage value increases, and the maximum
voltage can be reached. Moving in the opposite direction of the arrow,
the voltage value gradually decreases to the minimum voltage. In the
Y-axis direction, the voltage value decreases gradually as it moves in
the direction of the arrow on the module, decreasing to the minimum
voltage. As the arrow is moved in the opposite direction, the voltage
value increases and can reach the maximum voltage. In the Z-axis
direction, the signal terminal B is connected to the digital port and
outputs 0 in the original state and outputs 1 when pressed. In this way,
we can read the two analog values and the high and low level conditions
of the digital port to determine the operating status of the joystick on
the module.

**Features:**

Input Voltage：DC 3.3V \~ 5V

Output Signal：X/Y dual axis analog value +Z axis digital signal

[Range](javascript:;) [of](javascript:;) [Application](javascript:;)：Suitable
for control point coordinate movement in plane as well as control of two
degrees of freedom steering gear, etc.  

[product](javascript:;) [feature](javascript:;)s：Exquisite appearance,
joystick feel superior, simple operation, sensitive response, long
service life.

4. Read the value of the Rocker Module：

We must use ESP32’s analog IO port to read the value from the X/Y pin of
the rocker module and use the digital IO port to read the digital signal
of the button. Please connect the wires according to the wiring diagram
below：

![](/media/b611755eacc4c603e6c0555aced929cb.png)

You can open the code we provide:

The code used in this project is saved in folder**“2. Windows System\\2.
C\_Tutorial\\2. Projects\\Project 28：Rocker control
light\\Project\_28.1\_Read\_Rocker\_Value”**.

    //**********************************************************************************
    /*  
     * Filename    : Read Rocker Value
     * Description : Read data from Rocker.
     * Auther      : http//www.keyestudio.com
    */
    int xyzPins[] = {36, 39, 14};   //x,y,z pins
    void setup() {
      Serial.begin(115200);
      pinMode(xyzPins[0], INPUT); //x axis. 
      pinMode(xyzPins[1], INPUT); //y axis. 
      pinMode(xyzPins[2], INPUT_PULLUP);   //z axis is a button.
    }
    
    // In loop(), use analogRead () to read the value of axes X and Y 
    //and use digitalRead () to read the value of axis Z, then display them.
    void loop() {
      int xVal = analogRead(xyzPins[0]);
      int yVal = analogRead(xyzPins[1]);
      int zVal = digitalRead(xyzPins[2]);
      Serial.println("X,Y,Z: " + String(xVal) + ", " +  String(yVal) + ", " + String(zVal));
      delay(500);
    }
    //**********************************************************************************


Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable, open the serial monitor and set
the baud rate to 115200. You will see that the serial port monitor
window will print out the analog and digital values of the current
joystick. Moving the joystick or pressing it will change the analog and
digital values.

![](/media/06a9de681779df5cfc7e6bc24a928a3a.jpeg)

![](/media/d5feb7bddc603e96924276d47280dd94.png)

5. Wiring diagram of Rocker control light：

We just read the value of the rocker module, we need to do something
with the rocker module and RGB here, Follow the diagram below for
wiring：

![](/media/4ec49b488fedf216d03e49f83bc8443a.png)

6. Project code：

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\****2. C\_Tutorial\\2. Projects\\Project 28：Rocker control
light、Project\_28.2\_Rocker\_Control\_Light”**.

    //**********************************************************************************
    /*  
     * Filename    : Rocker Control Light
     * Description : Control RGB to light different colors by Rocker.
     * Auther      : http//www.keyestudio.com
    */
    int x_Pin = 36;   //x pin
    int y_Pin = 39;   //y pin
    int z_Pin = 14;   //z pin
    int ledPins[] = {4, 0, 2};    //define red, green, blue led pins
    const byte chns[] = {0, 1, 2};        //define the pwm channels
    
    void setup() {
      pinMode(x_Pin, INPUT); //x axis. 
      pinMode(y_Pin, INPUT); //y axis. 
      pinMode(z_Pin, INPUT_PULLUP);   //z axis is a button.
      for (int i = 0; i < 3; i++) {   //setup the pwm channels,1KHz,8bit
        ledcSetup(chns[i], 1000, 8);
        ledcAttachPin(ledPins[i], chns[i]);
      }
    }
    
    // In loop(), use analogRead () to read the value of axes X and Y 
    //and use digitalRead () to read the value of axis Z, then display them.
    void loop() {
      int xVal = analogRead(x_Pin);
      int yVal = analogRead(y_Pin);
      int zVal = digitalRead(z_Pin);
      if (xVal < 1000){
         ledcWrite(chns[0], 255); //Common cathode LED, high level to turn on the led.
         ledcWrite(chns[1], 0);
         ledcWrite(chns[2], 0);
       }
      else if (xVal > 3000){
         ledcWrite(chns[0], 0); 
         ledcWrite(chns[1], 255);
         ledcWrite(chns[2], 0);
       }
      else if (yVal < 1000){
         ledcWrite(chns[0], 0);
         ledcWrite(chns[1], 0);
         ledcWrite(chns[2], 255);
       }
      else if (yVal > 3000){
         ledcWrite(chns[0], 255); 
         ledcWrite(chns[1], 255);
         ledcWrite(chns[2], 255);
       }
    }
    //**********************************************************************************


7. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that ①If the
rocker is moved to the far left in the X direction, the RGB light turns
red. ② If the rocker is moved to the far right in the X direction, the
RGB light turns green. ③If the rocker is moved to the up in the Y
direction, the RGB light turns white. ④If the rocker is moved to the
down in the Y direction, the RGB light turns blue.

![](/media/9c2d0d8777200827b16c49b752d45c4c.jpeg)
