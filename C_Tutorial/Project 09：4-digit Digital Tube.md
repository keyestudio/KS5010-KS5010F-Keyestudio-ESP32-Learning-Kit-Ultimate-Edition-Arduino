# Project 09：4-Digit Digital Tube

1. Introduction：

A 4-digit 7-segment display is a very practical display device and it is
used for devices such as electronic clocks, score counters and the
number of people in the park. Because of the low price, easy to use,
more and more projects will use 4 Digit 7-segment display. In this
project, we use ESP32 control 4-digit 7-segment display to display four
digits.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:2.17847in;height:1.0625in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.94722in;height:2.32014in" /></td>
<td></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td></td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/f65653a12f286475b4365035aa12c7c0.png" style="width:1.90347in;height:0.97917in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/ece3c38dc9a9e6428b122481d6bb0d4d.png" style="width:1.19028in;height:1.00556in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.05903in;height:0.56667in" /></td>
</tr>
<tr class="even">
<td>4-digit 7-segment display Module*1</td>
<td>M-F Dupont Wires</td>
<td>USB Cable*1</td>
</tr>
</tbody>
</table>

3. Component knowledge：

**TM1650 4-digit 7-segment display：**It is a 12-pin 4-digit 7-segment
display module with clock dots. The driver chip is TM1650 which only
needs 2 signal lines to enable the microcontroller to control the
4-digit 7-segment display. The control interface level can be 5V or
3.3V.

**Specifications of 4-bit 7-segment display module:**

Working voltage: DC 3.3V-5V

Maximum current: 100MA

Maximum power: 0.5W

**Schematic diagram of 4-digit 7-segment display module:**

![](/media/5f400887c90fc00098a3e77beca656ef.png)

4. Wiring diagram：

![](/media/a7721c08ed3b73b21a997d43d2e3addd.png)

**5.Adding the TM1650 library：**

This code uses a library named "**TM1650**", if you haven't installed it
yet, please do so before learning. The steps to add third-party
libraries are as follows:

How to install the library？

Open the Arduino IDE，click “Sketch”→“Include Library”→“Add .ZIP
Library...”. In the pop-up window, find the file named **“2. Windows
System\\2. C\_Tutorial\\3. Libraries\\****TM1650.ZIP”** which locates in
this directory. Select the **TM1650.ZIP** file and then click“Open”.

![](/media/86b7835c0f2a2acf84e5da36d0175873.png)

![](/media/fff642761e9f7b83064374d0950f71ec.png)

5. Project code：

After the **TM1650** library is added, you can open the code we provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 09：4-Digit Digital
Tube\\Project\_09\_Four\_Digit\_Digital\_Tube”**.

    //**********************************************************************
    /* 
     * Filename    : 4-Digit Digital Tube
     * Description : Four Digit Tube displays numbers from 1111 to 9999.
     * Auther      : http//www.keyestudio.com
    */
    #include "TM1650.h"
    #define CLK 22    //pins definitions for TM1650 and can be changed to other ports 
    #define DIO 21
    TM1650 DigitalTube(CLK,DIO);
    
    void setup(){
      //DigitalTube.setBrightness();  //stes brightness from 0 to 7(default is 2)
      //DigitalTube.displayOnOFF();   // 0= off,1= on(default is 1)
      for(char b=1;b<5;b++){
        DigitalTube.clearBit(b);      //which bit to clear
      }
      DigitalTube.displayDot(1,true); // displays the first number
      DigitalTube.displayDot(2,true);
      DigitalTube.displayDot(3,true);
      DigitalTube.displayDot(4,true);
      DigitalTube.displayBit(3,0);    //which number to display. bit=1-4, number=0-9
    }
    
    void loop(){
      for(int num=0; num<10; num++){
        DigitalTube.displayBit(1,num);
        DigitalTube.displayBit(2,num);
        DigitalTube.displayBit(3,num);
        DigitalTube.displayBit(4,num);
        delay(1000);
      }  
     }
    //**********************************************************************************


7. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that 4-digit
7-segment display displays four digits，and repeat these actions in an
infinite loop.
