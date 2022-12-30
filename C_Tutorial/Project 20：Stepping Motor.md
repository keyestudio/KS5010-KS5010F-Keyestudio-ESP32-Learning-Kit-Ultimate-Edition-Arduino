# Project 20：Stepping Motor 

1. Introduction：

Stepper motor is the most important part of industrial robot 3D printer
lathes and other mechanical equipment with accurate positioning. In this
project, we will use ESP32 control ULN2003 stepper motor drive board to
drive the stepper motor to rotate.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:1.58264in;height:0.77292in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.84236in;height:2.06319in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/6c9c142fb9187aeb8337493ca5dd5ee7.jpeg" style="width:1.56111in;height:1.03819in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>ULN2003 Stepper Motor Drive Board*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/8ebb14a35091dc8d02d95cb6748dd1e9.png" style="width:0.93403in;height:0.92431in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/6ba5c3147b32861b2dbc6b9986382c1b.png" style="width:0.88681in;height:1.04722in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:0.99028in;height:0.52986in" /></td>
</tr>
<tr class="even">
<td>Stepper Motor *1</td>
<td>M-F Dupont Wires</td>
<td>USB Cable*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/b65d826ca481982fed0212dba2957c7c.jpeg" style="width:1.57361in;height:1.13611in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/a8fe41500d5d16511fd90518f745d398.png" style="width:1.80903in;height:0.78125in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/a815c48437199c6ab79d74cd2d583de0.png" style="width:0.41042in;height:1.89444in" /></td>
</tr>
<tr class="even">
<td>Battery Holder*1</td>
<td>Keyestudio bread board special power module*1</td>
<td>No.5 battery (self-provided)*6</td>
</tr>
</tbody>
</table>

3. Component knowledge：

![](/media/8ebb14a35091dc8d02d95cb6748dd1e9.png)

**Stepper motor:** It is a motor controlled by a series of
electromagnetic coils. It can rotate by the exact number of degrees (or
steps) needed, allowing you to move it to a precise position and keep it
there. It does this by supplying power to the coil inside the motor in a
very short time, but you must always supply power to the motor to keep
it in the position you want. There are two basic types of stepping
motors, namely unipolar stepping motor and bipolar stepping motor. In
this project, we use a 28-BYJ48 unipolar stepper motor.

![](/media/bea0e202b7bfe23d1fdcdbbe996aa6da.jpeg)

**Working Principle:**

The stepper motor is mainly composed of a stator and a rotor. The stator
is fixed. As shown in the figure below, the part of the coil group A, B,
C, and D will generate a magnetic field when the coil group is
energized. The rotor is the rotating part. As follows, the middle part
of the stator, two poles are permanent magnets.

![](/media/32748e0804b1fff434181cb228b23242.png)

Single -phase four beat: At the beginning, the coils of group A are
turned on, and the poles of the rotor point at A coil. Next, the group A
coil are disconnected, and the group B coils are turned on. The rotor
will turn clockwise to the group B. Then, group B is disconnected, group
C is turned on, and the rotor is turned to group C. After that, group C
is disconnected, and group D is turned on, and the rotor is turned to
group D. Finally, group D is disconnected, group A is turned on, and the
rotor is turned to group A coils. Therefore, rotor turns 180° and
continuously rotates B-C-D-A, which means it runs a circle (eight
phase). As shown below, he rotation principle of stepper motor is A - B
- C - D - A.

You make order inverse(D - C - B - A - D .....) if you want to make
stepper motor rotate anticlockwise.

![](/media/b8ae50bbdee2dd5bc683e8c450baee6a.png)

Half-phase and eight beat: 8 beat adopts single and dual beat way，A - AB
- B - BC - C - CD - D - DA - A ...... ，rotor will rotate half phase in
this order. For example, when A coil is electrified，rotor faces to A
coil , then A and B coil are connected, on this condition, the strongest
magnetic field produced lies in the central part of AB coil, which means
rotating half-phase clockwise.

**Stepper Motor Parameters:**

The rotor rotates one circle when the stepper motor we provide rotates
32 phases and with the output shaft driven by 1:64 reduction geared set.
Therefore the rotation (a circle) of output shaft requires 32 \* 64 =
2048 phases.

The step angle of 4-beat mode of 5V and 4-phase stepper motor is 11.25.
And the step angle of 8-beat mode is 5.625, the reduction ratio is 1:64.

**ULN2003Stepper Motor Drive Board:** It is a stepper motor driver,
which converts the weak signal into a stronger control signal to drive
the stepper motor. 

The following schematic diagram shows how to use the ULN2003 stepper
motor driver board interface to connect a unipolar stepper motor to the
pins of the ESP32, and shows how to use four TIP120 interfaces.

![](/media/6fa632d2b70e97dd55565d23ec15d245.png)

4. Wiring Diagram：

![](/media/6333a59ee8dd57f7ceb5eaaec8d588df.png)

5. Project code：

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\****2. C\_Tutorial\\2. Projects\\Project 20：Stepping
Motor\\Project\_20\_Stepping\_Motor”**.

    //**********************************************************************
    /*
     * Filename    : Drive Stepper Motor
     * Description : Use ULN2003 to drive the stepper motor.
     * Auther      : http//www.keyestudio.com
    */
    // Conncet the port of the stepper motor driver
    int outPorts[] = {15, 16, 17, 18};
    
    void setup() {
      // set pins to output
      for (int i = 0; i < 4; i++) {
        pinMode(outPorts[i], OUTPUT);
      }
    }
    
    void loop()
    {
      // Rotate a full turn
      moveSteps(true, 32 * 64, 3);
      delay(1000);
      // Rotate a full turn towards another direction
      moveSteps(false, 32 * 64, 3);
      delay(1000);
    }
    
    //Suggestion: the motor turns precisely when the ms range is between 3 and 20
    void moveSteps(bool dir, int steps, byte ms) {
      for (unsigned long i = 0; i < steps; i++) {
        moveOneStep(dir); // Rotate a step
        delay(constrain(ms,3,20));        // Control the speed
      }
    }
    
    void moveOneStep(bool dir) {
      // Define a variable, use four low bit to indicate the state of port
      static byte out = 0x01;
      // Decide the shift direction according to the rotation direction
      if (dir) {  // ring shift left
        out != 0x08 ? out = out << 1 : out = 0x01;
      }
      else {      // ring shift right
        out != 0x01 ? out = out >> 1 : out = 0x08;
      }
      // Output singal to each port
      for (int i = 0; i < 4; i++) {
        digitalWrite(outPorts[i], (out & (0x01 << i)) ? HIGH : LOW);
      }
    }
    
    void moveAround(bool dir, int turns, byte ms){
      for(int i=0;i<turns;i++)
        moveSteps(dir,32*64,ms);
    }
    void moveAngle(bool dir, int angle, byte ms){
      moveSteps(dir,(angle*32*64/360),ms);
    }
    //********************************************************************************


6. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that the four
LEDs ( D1,D2,D3 ,D4) on the ULN2003 drive module will light up. The
stepper motor rotates clockwise first, then counterclockwise, and repeat
these actions in an endless loop.

![](/media/8dc4a0547390e0108c3960c31d330ee7.png)
