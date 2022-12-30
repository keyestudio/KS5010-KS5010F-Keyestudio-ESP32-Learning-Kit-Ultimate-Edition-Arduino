# Project 06: RGB LED

1. Introduction：

![](/media/94bdff69e438989d8e0934e57f2e5c00.png)

RGB is composed of three colors (red, green and blue),which can emit
different colors of light by mixing these three basic colors.

In this project, we will introduce the RGB and show you how to use ESP32
to control the RGB to emit different color light .RGB is pretty basic,
but it’s also a great way to learn the fundamentals of electronics and
coding.

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
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/f1a86fc81ab4b043263ce7e01e14d470.png" style="width:0.23056in;height:1.27847in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/098a2730d0b0a2a4b2079e0fc87fd38b.png" style="width:1.22639in;height:0.49236in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/c801a7baee258ff7f5f28ac6e9a7097b.png" style="width:0.66736in;height:0.64097in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.05903in;height:0.56667in" /></td>
</tr>
<tr class="even">
<td>RGB LED*1</td>
<td>220Ω Resistor*3</td>
<td>Jumper Wires</td>
<td>USB Cable*1</td>
</tr>
</tbody>
</table>

3. Component knowledge：

Most monitors adopt the RGB color standard, and all colors on a computer
screen are a mixture of red, green and blue in varying proportions.

![](/media/8bf1339719a922f2fbc1e01a4347b4ab.png)

This RGB LED has 4 pins, each color (red, green, blue) and a common
cathode,To change its brightness, we can use the PWM of the ESP32 pins,
which can give different duty cycle signals to the RGB to produce
different colors of light.

If we use three 10-bit PWM to control the RGB, in theory, we can create
2 <sup>10</sup>\*2<sup>10</sup>\*2<sup>10</sup> =1,073,741,824(1billion)
colors through different combinations.

4. Wiring diagram：

![](/media/f3deb3502985ac8d66e99e4f27b3de1e.png)

**Note:**

How to connect a LED

![](/media/42ff6f405dfa128593827de5aa03e94b.png)

How to identify the 220Ω Five-color ring resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

5. Project code：

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 06：RGB
LED\\Project\_06\_RGB\_LED”**.

    //**********************************************************************
    /*
     * Filename    : RGB LED
     * Description : Use RGBLED to show random color.
     * Auther      : http//www.keyestudio.com
    */
    int ledPins[] = {0, 2, 15};    //define red, green, blue led pins
    const byte chns[] = {0, 1, 2};        //define the pwm channels
    int red, green, blue;
    void setup() {
      for (int i = 0; i < 3; i++) {   //setup the pwm channels,1KHz,8bit
        ledcSetup(chns[i], 1000, 8);
        ledcAttachPin(ledPins[i], chns[i]);
      }
    }
    
    void loop() {
      red = random(0, 256);
      green = random(0, 256);
      blue = random(0, 256);
      setColor(red, green, blue);
      delay(200);
    }
    
    void setColor(byte r, byte g, byte b) {
      ledcWrite(chns[0], 255 - r); //Common anode LED, low level to turn on the led.
      ledcWrite(chns[1], 255 - g);
      ledcWrite(chns[2], 255 - b);
    }
    //*************************************************************************************


6. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that the RGB
LED starts to display random colors.
