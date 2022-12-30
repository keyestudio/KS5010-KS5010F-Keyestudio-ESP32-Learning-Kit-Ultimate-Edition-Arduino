# Project 21：Relay

1. Introduction：

In our daily life, we usually use communication to drive electrical
equipments, and sometimes we use switches to control electrical
equipments. If the switch is connected directly to the ac circuit,
leakage occurs and people are in danger. Therefore, from the
perspective of safety, we specially designed this relay module with
NO(normally open) end and NC(normally closed) end. In this project,
we will learn a relatively special and easy-to-use switch, which is
the relay module.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7a4832b8ab8659c061b37c4614793e3e.jpeg" style="width:1.17014in;height:0.57153in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.55417in;height:1.35972in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/1ea87894c6aa8d475203e447ad5e930a.png" style="width:1.38056in;height:0.73958in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/6ba5c3147b32861b2dbc6b9986382c1b.png" style="width:0.88681in;height:1.04722in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.11528in;height:0.59722in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>Relay Module*1</td>
<td>M-F Dupont Wires</td>
<td>USB Cable*1</td>
</tr>
</tbody>
</table>

3. Component knowledge：

**Relay:** It is an "automatic switch" that uses a small current to
control the operation of a large current.

Input voltage：3.3V-5V

Rated load：5A 250VAC (NO/NC) 5A 24VDC (NO/NC)

The rated load means that devices with dc voltage of 24V or AC voltage
of 250V can be controlled using 3.3V-5V microcontrollers.

**Schematic diagram of Relay：**

![](/media/be1c90d2b52fc2489590e3f702a087bf.emf)

4. Wiring Diagram：

![](/media/1741d3cb0405c740378ef7ef96df6072.png)

5. Project code：

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project
21：Relay\\Project\_21\_Relay”**.

    //**********************************************************************************
    /*
     * Filename    : Relay
     * Description : Relay turn on and off.
     * Auther      : http//www.keyestudio.com
    */
    #define  Relay  15 // defines digital 15
    void setup()
    {
    pinMode(Relay, OUTPUT); // sets "Relay" to "output"
    }
    void loop()
    {
    digitalWrite(Relay, HIGH); // turns on the relay
    delay(1000); //delays 1 seconds
    digitalWrite(Relay, LOW); // turns off the relay
    delay(1000); // delays 1 seconds
    }
    //**********************************************************************************


6. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that the relay
will cycle on and off, on for 1 second, off for 1 second.  At the same
time, you can hear the sound of the relay on and off, and you can also
see the change of the indicator light on the relay.
