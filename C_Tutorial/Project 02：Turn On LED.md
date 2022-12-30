# Project 02: Turn On LED

1. Introduction：

In this project, we will show you how to light up the LED. We use the
ESP32's digital pin to turn on the LED so that the LED is lit up.

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

**（1）LED:**

![](/media/081141eed6146deed2bfbd8e55a8465b.jpeg)

The LED is a semiconductor known as “light-emitting diode” ,which is an
electronic device made from semiconducting materials(silicon, selenium,
germanium, etc.). It has an anode and a cathode, the short lead is
cathode, which connects to GND; the long lead is anode, which connects
to3.3V or 5V.

![](/media/f70404aa49540fd7aecae944c7c01f83.jpeg)

**（2）Five-color ring resistor**

A resistor is an electronic component in a circuit that restricts or
regulates the flow current flow. On the left is the appearance of the
resistor and on the right is the symbol for the resistance in the
circuit . Its unit is(Ω). 1 mΩ= 1000 kΩ，1kΩ= 1000Ω.

![](/media/8a86f65cf820d08e8956daa70d1c4195.jpeg)
![](/media/f6079fe22518f0fc1b0c3a3b93a516a1.png)

We can use resistors to protect sensitive components, such as LED. The
strength of the resistance is marked on the body of the resistor with an
electronic color code. Each color code represents a number, and you can
refer to it in a resistance card.

\-Color 1 – 1st Digit.

\-Color 2 – 2nd Digit.

\-Color 3 – 3rd Digit.

\-Color 4 – Multiplier.

\-Color 5 – Tolerance.

![](/media/c3df005312cd9f6d4cdae6abf3cddb83.png)

In this kit, we provide three Five-color ring resistor with different
resistance values. Take three Five-color ring resistor as an example.

220Ω Resistor\*10

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

10KΩ Resistor\*10

![](/media/246cf3885dc837c458a28123885c9f7b.png)

1KΩ Resistor\*10

![](/media/19f5dfc51adfd79b04c3b164529767ed.png)

In the same voltage, there will be less current and more resistance. The
connection between current(I), voltage(V), and resistance(R) can be
expressed by the formula: I=U/R. In the figure below, if the voltage is
3V, the current through R1 is: I = U / R = 3 V / 10 KΩ= 0.0003A= 0.3mA.

![](/media/b3eec552e4dfad361833730698621776.png)

Don’t connect a low resistance directly to the two poles of the power
supply. as this will cause excessive current to damage the electronic
components. Resistors do not have positive and negative poles.

**（3）Bread board**

Breadboards are used to build and test circuits quickly before
completing any circuit design. There are many holes in the breadboard
that can be inserted into circuit components such as integrated circuits
and resistors. A typical breadboard is shown below：

![](/media/612c1381811b2d780d5f6ed6a7ec3701.png)

The breadboard has strips of metal , which run underneath the board and
connect the holes on the top of the board. The metal strips are laid out
as shown below. Note that the top and bottom rows of holes are connected
horizontally，while the remaining holes are connected vertically.

![](/media/b45e70b961537035c85878b73d371725.png)

The first two rows (top) and the last two rows (bottom) of the
breadboard are used for the positive pole (+) and negative pole (-) of
the power supply respectively. The conductive layout of the breadboard
is shown in the figure below:

![](/media/d5478bd5eac558252cbc235479d979eb.png)

When we connect DIP (Dual In-line Packages) components, such as
integrated circuits, microcontrollers, chips and so on, we can see that
a groove in the middle isolates the middle part, so the top and bottom
of the groove is not connected. DIP components can be connected as shown
in the following diagram:

![](/media/50caf14e911c4244779e99445c658db6.png)

![](/media/9b66ae2199e77fbc99b7b278dac0b567.png)

4 [Power](javascript:;) [Supply](javascript:;)

The ESP32 needs 3.3V-5V power supply. In this project, we connected
the ESP32 to the computer by using a USB cable.

![](/media/56053f7126905c6def63919c661d5c0a.jpeg)

4. Wiring diagram：

First, disconnect all power from the ESP32. Then build the circuit
according to the wiring diagram. After the circuit is built and verified
correct, connect the ESP32 to your computer by using a USB cable.

**Note:** Avoid any possible short circuits (especially connecting 3.3V
and GND)\!

**WARNING:** A short circuit can cause high current in your circuit,
create excessive component heat and cause permanent damage to your
hardware\!

![](/media/0735997593c8858ad6441d8e9867206f.png)

Note:

How to connect a LED

![](/media/42ff6f405dfa128593827de5aa03e94b.png)

How to identify the 220Ω Five-color ring resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

5. Project code：

You can open the code we provide：

The code used in this project is saved in folder(path:)**“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 02：Turn On
LED\\Project\_02\_Turn\_On\_LED”**.

    //**********************************************************************
    /*
     * Filename    : Turn On LED
     * Description : Make an led on.
     * Auther      : http//www.keyestudio.com
    */
    #define LED_BUILTIN 15
    
    // the setup function runs once when you press reset or power the board
    void setup() {
      // initialize digital pin LED_BUILTIN as an output.
      pinMode(LED_BUILTIN, OUTPUT);
    }
    void loop() {
      digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
    }
    //*************************************************************************************


Before uploading the project code to ESP32，click“Tools”→“Board” and
select“ESP32 Wrover Module”.

![](/media/fe6528f9ab19545157bcf59199004ba0.png)

Select the serial port.

![](/media/e4ea8ba2d933a8057dadff0ca03c7b8a.png)

**Note:** For macOS users, if the uploading fails, please set the baud
rate to 115200 before clicking![](/media/b0d41283bf5ae66d2d5ab45db15331ba.png).

![](/media/ea1414f745b5f809a1ef64926a67ad5c.png)

Click![](/media/b0d41283bf5ae66d2d5ab45db15331ba.png)to download the code to ESP32.

![](/media/b767b8a640084e084d12081f41f292c2.png)

**Note:** If uploading the code fails, you can press the Boot button on
ESP32 after click![](/media/d09c4a31563f04a42d451e7bc1a5fb8a.png), and release the Boot
button![](/media/dc77bfcf5851c8f43aab6cbe7cec7920.png) after the percentage of uploading progress
appears, as shown below:

![](/media/157ee2e7687559d9812d24edec758150.png)

The Project code is uploaded successfully！

![](/media/8c07abd2d992c043f1a2faef6c903057.png)

6. Project result：

After the project code was uploaded successfully, power up with a USB
cable and the LED is lit up.

![](/media/77dec960e108229b6d97b4af9a2db902.png)
