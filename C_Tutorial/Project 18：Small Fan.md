# Project 18：Small Fan

1. Introduction：

In hot summer, we need electric fans to cool us down, so in this
project, we will use ESP32 control 130 motor module and small fan blade
to make a small electric fan.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:2.17847in;height:1.0625in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.74792in;height:1.83333in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/b65d826ca481982fed0212dba2957c7c.jpeg" style="width:1.57361in;height:1.13611in" /></td>
<td></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>Battery Holder*1</td>
<td></td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/4dc1472ab8d2cf85fd7518646e10d0ee.png" style="width:1.16944in;height:0.5in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e07904c75497330fe5abe3b5c21d4d02.png" style="width:1.39653in;height:0.60278in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/ece3c38dc9a9e6428b122481d6bb0d4d.png" style="width:0.96667in;height:0.81667in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/a815c48437199c6ab79d74cd2d583de0.png" style="width:0.28611in;height:1.31944in" /></td>
</tr>
<tr class="even">
<td>130 Motor Module*1</td>
<td>Keyestudio bread board special power module*1</td>
<td>M-F Dupont Wires</td>
<td>No.5 battery (self-provided)*6</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/009965e315276ecf1144c22c54a93fd9.png" style="width:0.94375in;height:0.82986in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:0.83542in;height:0.44722in" /></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Fan*1</td>
<td>USB Cable*1</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

3. Component knowledge :

![](/media/75a9140bdb671783bb79a71ca76fae69.png)

**130 motor module:** The motor control module uses the HR1124S motor
control chip. which is a single-channel H-bridge driver chip for DC
motor.. The H-bridge driver part of the HR1124S uses low on-resistance
PMOS and NMOS power tubes. The low on-resistance ensure low power loss
of the chip and make the chip work safely for longer time In addition,
In addition, the HR1124S has low standby current and low static
operating current, which makes the HR1124S easy to use in toy solutions.

**Features:**

Working voltage: 5V

Working current: 200MA

Working power: 2W

Working temperature: -10℃\~ +50℃

**Schematic diagram of 130 motor module：**

![](/media/ee2deb2ed7ae310b953ff178aff3d6c1.emf)

**Keyestudio Breadboard Power Supply Module：**

![](/media/7ff03f4506988f1ce99c5757892fc6de.jpeg)

**Introduction:**

This breadboard power supply module is compatible with 5V and 3.3V,
which can be applied to MB102 breadboard. The module contains two
channels of independent control, powered by the USB all the way.

The output voltage is constant for the DC5V, and another way is powered
by DC6.5-12V, output controlled by the slide switch, respectively for
DC5V and DC3.3V.

If the other power supply is DC 6.5-12v, when the slide switch is
switched to +5V, the output voltages of the left and right lines of the
module are DC 5V. When the slide switch is switched to +3V, the output
voltage of the USB power supply terminal of the module is DC5V , and the
output voltage of the DC 6.5-12V power supply terminal of the other
power supply is DC3.3V.

**Specification:**

- Applied to MB102 breadboard;

- Input voltage：DC 6.5-12V or powered by USB;

- Output voltage：3.3V or 5V

- Max output current：\<700ma

- Up and down two channels of independent control, one of which can be
switched to 3.3V or 5V;

Comes with two sets of DC output pins, easy for external use.

4. Wiring Diagram：

![](/media/83f622be72c1b5501ffeab7bd1caf421.png)

(Note: Connect the wires and then install a small fan blade on the
DC motor. )

<!-- end list -->

5. Project code：

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\****2. C\_Tutorial\\2. Projects\\Project 18：Small
Fan\\Project\_18\_ Small\_Fan”**.

    //**********************************************************************************
    /*
     * Filename    : Small Fan
     * Description : Fan clockwise rotation,stop,counterclockwise rotation,stop,cycle.
     * Auther      : http//www.keyestudio.com
    */
    #define Motorla    15  // the Motor_IN+ pin of the motor
    #define Motorlb     2  // the Motor_IN- pin of the motor
    
    void setup(){
      pinMode(Motorla, OUTPUT);//set Motorla to OUTPUT
      pinMode(Motorlb, OUTPUT);//set Motorlb to OUTPUT
    }
    void loop(){
    //Set to rotate for 5s anticlockwise
      digitalWrite(Motorla,HIGH);
      digitalWrite(Motorlb,LOW);
      delay(5000);
    //Set to stop rotating for 2s 
      digitalWrite(Motorla,LOW);
      digitalWrite(Motorlb,LOW);
      delay(2000);
    //Set to rotate for 5s clockwise
      digitalWrite(Motorla,LOW);
      digitalWrite(Motorlb,HIGH);
      delay(5000);
    //Set to stop rotating for 2s 
      digitalWrite(Motorla,LOW);
      digitalWrite(Motorlb,LOW);
      delay(2000);
    }
    //********************************************************************************


6. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see thatthe small
fan turns counterclockwise for 5 seconds and stops for 2 seconds, and
then turns clockwise for 5 seconds and stops for 2 seconds, which
repeats in an endless loop.
