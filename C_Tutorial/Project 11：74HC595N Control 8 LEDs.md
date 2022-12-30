# Project 11：74HC595N Control 8 LEDs 

1. Introduction：

In previous projects, we learned how to light up an LED.

With only 32 IO ports on ESP32, how do we light up a lot of
leds? Sometimes it is possible to run out of pins on the ESP32, and you
need to extend it with the shift register.You can use the 74HC595N chip
to control 8 outputs at a time, taking up only a few pins on your
microcontroller. In addition, you can also connect multiple registers
together to further expand the output. In this project, we will use
ESP32、74HC595 chip and LED to make a flowing water light to understand
the function of the 74HC595 chip.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/2a55dec25d757def2b46d5e9cd9c97e5.jpeg" style="width:1.75972in;height:0.85833in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.63889in;height:1.56667in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/f97e58ab51ec0a274ff3e72e08a7d55d.png" style="width:1.07847in;height:0.88611in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/c801a7baee258ff7f5f28ac6e9a7097b.png" style="width:0.98958in;height:0.95139in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>74HC595N chip*1</td>
<td>Jumper Wires</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/098a2730d0b0a2a4b2079e0fc87fd38b.png" style="width:1.22639in;height:0.49236in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/3ec5906fad2172708d449390140f55e6.png" style="width:0.28056in;height:1.19722in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.05903in;height:0.56667in" /></td>
<td></td>
</tr>
<tr class="even">
<td>220ΩResistor*8</td>
<td>Red LED*8</td>
<td>USB Cable*1</td>
<td></td>
</tr>
</tbody>
</table>

3. Component knowledge：

![](/media/6921c6d60135e072ed4bd24564ec4a6d.png)

**74HC595N Chip:** The 74HC595 chip is used to convert serial data into
parallel data. A 74HC595 chip can convert the serial data of one byte
into 8 bits, and send its corresponding level to each of the 8 ports
correspondingly. With this characteristic, the 74HC595 chip can be used
to expand the IO ports of an ESP32. At least 3 ports are required to
control the 8 ports of the 74HC595 chip.

![](/media/858b189f06ad68afe051b15043b2affd.png)

The ports of the 74HC595 chip are described as follows ：

<table>
<tbody>
<tr class="odd">
<td>Pin 13--OE</td>
<td><p>Enable output,</p>
<p>When this pin is in high level, Q0-Q7 is in high resistance state.</p>
<p>When this pin is in low level, Q0-Q7 is in output mode.</p></td>
</tr>
<tr class="even">
<td>Pin 14---SI</td>
<td>Serial data Input, only enter one bit at a time, so you can enter eight consecutive times to form one byte.</td>
</tr>
<tr class="odd">
<td>Pin 10---SCLR</td>
<td>Remove shift register: When this pin is in low level, the content in shift register will be cleared.. In this experiment, we connect VCC to maintain a high level.</td>
</tr>
<tr class="even">
<td>Pin 11---SCK</td>
<td>Serial shift clock: when its electrical level is rising, serial data input register will do a shift.</td>
</tr>
<tr class="odd">
<td>Pin 12---RCK</td>
<td>Parallel Update Output: when its electrical level is rising, it will update the parallel data output. In this case, the data is output from ports Q0 to Q7 in parallel</td>
</tr>
<tr class="even">
<td>Pin 9---SQH</td>
<td>Serial data output: it can be connected to more 74HC595 in series.</td>
</tr>
<tr class="odd">
<td>Q0--Q7(Pin 15，Pin 1-7)</td>
<td>Parallel data output, can directly control the 8 segments of the digital tube.</td>
</tr>
</tbody>
</table>

4. Wiring diagram：

Note: Note the orientation in which the 74HC595N chip is inserted.

![](/media/a6d03617539b70d6d69fa7e9acb25be9.png)

![](/media/11a03579b6cf94599f00554bfe014a3b.png)

5. Project code：

You can open the code we provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 11：74HC595N Control 8
LEDs\\Project\_11\_74HC595N\_Control\_8\_LEDs****”**.

    //**********************************************************************
    /* 
     * Filename    : 74HC595N Control 8 LEDs
     * Description : Use 74HC575N to drive ten leds to display the flowing light.
     * Auther      : http//www.keyestudio.com
    */
    int dataPin = 14;   // Pin connected to DS of 74HC595(Pin14)  
    int latchPin = 12;  // Pin connected to ST_CP of 74HC595(Pin12)
    int clockPin = 13;  // Pin connected to SH_CP of 74HC595(Pin11)          
    
    
    void setup() {
      // set pins to output
      pinMode(latchPin, OUTPUT);
      pinMode(clockPin, OUTPUT);
      pinMode(dataPin, OUTPUT);
    }
    
    void loop() {
      // Define a one-byte variable to use the 8 bits to represent the state of 8 LEDs of LED bar graph.
      // This variable is assigned to 0x01, that is binary 00000001, which indicates only one LED light on.
      byte x = 0x01;    // 0b 0000 0001
      for (int j = 0; j < 8; j++) { // Let led light up from right to left
        writeTo595(LSBFIRST, x);
        x <<= 1; // make the variable move one bit to left once, then the bright LED move one step to the left once.
        delay(50);
      }
      delay(100);
      x = 0x80;       //0b 1000 0000
      for (int j = 0; j < 8; j++) { // Let led light up from left to right
        writeTo595(LSBFIRST, x);
        x >>= 1;    
        delay(50);
      }
      delay(100);
    }
    void writeTo595(int order, byte _data ) {
      // Output low level to latchPin
      digitalWrite(latchPin, LOW);
      // Send serial data to 74HC595
      shiftOut(dataPin, clockPin, order, _data);
      // Output high level to latchPin, and 74HC595 will update the data to the parallel output port.
      digitalWrite(latchPin, HIGH);
    }
    //**********************************************************************************


6. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that the 8 LEDs
start flashing in flowing water mode.
