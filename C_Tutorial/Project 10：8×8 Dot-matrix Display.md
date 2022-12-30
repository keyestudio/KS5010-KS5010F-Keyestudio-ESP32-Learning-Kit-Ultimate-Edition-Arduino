# Project 10：8×8 Dot-matrix Display

1. Introduction：

Dot matrix display is an electronic digital display device that can
display information on machine, clocks, public transport departure
indicators and many other devices. In this project, we will use ESP32
control 8x8 LED dot matrix to display patterns.

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
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/fa4eb4c55bbbb4ae7fcde8298a903b5a.png" style="width:1.71875in;height:0.85694in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/ece3c38dc9a9e6428b122481d6bb0d4d.png" style="width:1.19028in;height:1.00556in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.05903in;height:0.56667in" /></td>
</tr>
<tr class="even">
<td>8*8 dot matrix module*1</td>
<td>M-F Dupont Wires</td>
<td>USB Cable*1</td>
</tr>
</tbody>
</table>

3. Component knowledge：

**8\*8 dot matrix module：**The 8\*8 dot matrix is composed of 64 LEDs,
and each LED is placed at the intersection of a row and a column. When
using the single chip microcomputer to drive an 8\*8 dot matrix, we need
16 digital ports in total, which greatly wastes the data of the single
chip microcomputer.To this end, we specially designed this module, using
the HT16K33 chip to drive an 8\*8 dot matrix, and only need to use the
I2C communication port of the MCU to control the 8\*8 dot matrix, which
greatly saving the MCU resources.

**Specifications of 8\*8 dot matrix module：**

Working voltage: DC 5V

Current: 200MA

Maximum power: 1W

**Schematic diagram of 8\*8 dot matrix module：**

![](/media/b04fe5e60695365a23644395aaef5085.png)

Some modules have three DIP switches that you can toggle at will. These
switches are used to set the I2C communication address, the setting
method is as follows. The module has fixed the communication address.
A0, A1 and A2 are connected to GND, and the address is 0x70.

<table>
<tbody>
<tr class="odd">
<td>A0（1）</td>
<td>A1（2）</td>
<td>A2（3）</td>
<td>A0（1）</td>
<td>A1（2）</td>
<td>A2（3）</td>
<td>A0（1）</td>
<td>A1（2）</td>
<td>A2（3）</td>
</tr>
<tr class="even">
<td>0（OFF）</td>
<td>0（OFF）</td>
<td>0（OFF）</td>
<td>1（ON）</td>
<td>0（OFF）</td>
<td>0（OFF）</td>
<td>0（OFF）</td>
<td>1（ON）</td>
<td>0（OFF）</td>
</tr>
<tr class="odd">
<td>0X70</td>
<td>0X71</td>
<td>0X72</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>A0（1）</td>
<td>A1（2）</td>
<td>A2（3）</td>
<td>A0（1）</td>
<td>A1（2）</td>
<td>A2（3）</td>
<td>A0（1）</td>
<td>A1（2）</td>
<td>A2（3）</td>
</tr>
<tr class="odd">
<td>1（ON）</td>
<td>1（ON）</td>
<td>0（OFF）</td>
<td>0（OFF）</td>
<td>0（OFF）</td>
<td>1（ON）</td>
<td>1（ON）</td>
<td>0（OFF）</td>
<td>1（ON）</td>
</tr>
<tr class="even">
<td>0X73</td>
<td>0X74</td>
<td>0X75</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>A0（1）</td>
<td>A1（2）</td>
<td>A2（3）</td>
<td>A0（1）</td>
<td>A1（2）</td>
<td>A2（3）</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>0（OFF）</td>
<td>1（ON）</td>
<td>1（ON）</td>
<td>1（ON）</td>
<td>1（ON）</td>
<td>1（ON）</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>0X76</td>
<td>0X77</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

4. Wiring diagram：

![](/media/78a74a4a920791b492bcd398dc8dc82b.png)

5. Adding the HT16K33\_Lib\_For\_ESP32 library：

This code uses a library named "**HT16K33\_Lib\_For\_ESP32**", if you
haven't installed it yet, please do so before learning.

How to install the library？

Open the Arduino IDE，click“Sketch”→“Include Library”→“Add .ZIP
Library...”. In the pop-up window, find the file named **“2. Windows
System\\2. C\_Tutorial\\3.Libraries\\****HT16K33\_Lib\_For\_ESP32.ZIP”**
which locates in this directory. Select the
**HT16K33\_Lib\_For\_ESP32.ZIP** file and then click“Open”.

![](/media/3c8e1110a11abb40613935fb9805990e.png)

![](/media/f79d0eb8aceb21234f7ee177114519fd.png)

6. Project code：

After the **HT16K33\_Lib\_For\_ESP32** library is added, you can open
the code we provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 10：8×8 Dot-matrix
Display\\Project\_10\_8×8\_Dot\_Matrix\_Display”**.

    //**********************************************************************************
    /*
     * Filename    : 8×8 Dot-matrix Display
     * Description : 8x8 LED dot matrix display“Heart” pattern.
     * Auther      : http//www.keyestudio.com
    */
    #include "HT16K33_Lib_For_ESP32.h"
    
    #define SDA 21
    #define SCL 22
    
    ESP32_HT16K33 matrix = ESP32_HT16K33();
    
    //The brightness values can be set from 1 to 15, with 1 darkest and 15 brightest
    #define  A  15
    
    byte result[8][8];
    byte test1[8] = {0x00,0x42,0x41,0x09,0x09,0x41,0x42,0x00};
    
    void setup()
    {
      matrix.init(0x70, SDA, SCL);//Initialize matrix
      matrix.showLedMatrix(test1,0,0);
      matrix.show();
    }
    
    void loop()
    {
      for (int i = 0; i <= 7; i++)
      {
        matrix.setBrightness(i);
        delay(100);
      }
      for (int i = 7; i > 0; i--)
      {
        matrix.setBrightness(i);
        delay(100);
      }
    }
    //**********************************************************************************


7. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that the 8\*8
dot matrix display“Smiling face”pattern.
