# Project 34：IR Control Sound and LED

1. Introduction：

An infrared(IR) remote control is a low-cost and easy-to-use wireless
communication technology. IR light is very similar to visible light,
except that its wavelength is slightly longer. This means that infrared
rays cannot be detected by the human eye, which is perfect for wireless
communication. For example, when you press a button on the TV remote
control, an infrared LED will switch on and off repeatedly at a
frequency of 38,000 times per second, transmitting information (such as
volume or channel control) to the infrared sensor on the TV.

We'll start by explaining how common infrared communication protocols
work. Then we will start the project with a remote control and an
infrared receiver component.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/146cead9d42f214abdbcd383a95eb998.jpeg" style="width:1.41458in;height:0.69097in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.55278in;height:1.35486in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/88e6b057fb4b0c576c9b2111d15b26e5.png" style="width:1.14861in;height:0.48403in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/f1a86fc81ab4b043263ce7e01e14d470.png" style="width:0.23056in;height:1.27847in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>IR Receiver *1</td>
<td>RGB LED*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/8a6fb37dedef748e6c2609bff5c64906.png" style="width:0.69792in;height:1.45764in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/4b4f653a76a82a3b413855493cc58fba.png" style="width:0.86111in;height:0.70069in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/a22dac8c5edbe90e867cbb04769d1816.png" style="width:0.23194in;height:1.04028in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/098a2730d0b0a2a4b2079e0fc87fd38b.png" style="width:1.22639in;height:0.49236in" /></td>
</tr>
<tr class="even">
<td>IR Remote Controller*1</td>
<td>Active buzzer*1</td>
<td>10KΩResistor*1</td>
<td>220ΩResistor*3</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/9197d4aff9356c585b7ef68e33a6881d.png" style="width:0.27986in;height:1.08819in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/098a2730d0b0a2a4b2079e0fc87fd38b.png" style="width:0.90833in;height:0.23681in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e9a8d050105397bb183512fb4ffdd2f6.png" style="width:0.90694in;height:0.90139in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:0.99028in;height:0.52986in" /></td>
</tr>
<tr class="even">
<td>NPN transistor(S8050)*1</td>
<td>1kΩResistor*1</td>
<td>Jumper Wires</td>
<td>USB Cable*1</td>
</tr>
</tbody>
</table>

3. Component knowledge：

**Infrared Remote：**An infrared(IR) remote control is a device with a
certain number of buttons. Pressing down different buttons will make the
infrared emission tube, which is located in the front of the remote
control, send infrared ray with different command. Infrared remote
control technology is widely used in electronic products such as
TV、airconditioning, etc. Thus making it possible for you to switch TV
programs and adjust the temperature of the air conditioning when away
from them. The remote control we use is shown below:

The infrared remote controller adopts NEC code and the signal cycle is
110ms.

![](/media/3c9d76cb0d24d9861811ce2cb0bb6ae4.png)

**Infrared receiver：**receiver is a component which can receive the
infrared light, so we can use it to detect the signal emitted by the
infrared remote control.

The infrared receiver demodules the received infrared signal and
converts it back to binary, then passes the information to the
microcontroller.

**Infrared signal modulation process diagram：**

![](/media/3da1969e509f53706643c77d0534eb73.png)

**NEC Infrared communication protocol：**

**NEC Protocol:**

To my knowledge the protocol I describe here was developed by NEC (Now
Renesas). I've seen very similar protocol descriptions on the internet,
and there the protocol is called Japanese Format.  
I do admit that I don't know exactly who developed it. What I do know is
that it was used in my late VCR produced by Sanyo and was marketed under
the name of Fisher. NEC manufactured the remote control IC.  
This description was taken from my VCR's service manual. Those were the
days, when service manuals were filled with useful information\!

**Features:**

- > \* 8 bit address and 8 bit command length.

- > \* Extended mode available, doubling the address size.

- > \* Address and command are transmitted twice for reliability.

- > \* Pulse distance modulation.

- > \* Carrier frequency of 38kHz.

- > \* Bit time of 1.125ms or 2.25ms.

**Modulation:**

![](/media/da33571c6f0afb94b1ec1d91caba3edb.png)

The NEC protocol uses pulse distance encoding of the bits. Each pulse is
a 560µs long 38kHz carrier burst (about 21 cycles). A logical "1" takes
2.25ms to transmit, while a logical "0" is only half of that, being
1.125ms. The recommended carrier duty-cycle is 1/4 or 1/3.

**Protocol:**

![](/media/f970404e7bbfb5711fea5c776f689f3a.png)

The picture above shows a typical pulse train of the NEC protocol. With
this protocol the LSB is transmitted first. In this case Address $59 and
Command $16 is transmitted. A message is started by a 9ms AGC burst,
which was used to set the gain of the earlier IR receivers. This AGC
burst is then followed by a 4.5ms space, which is then followed by the
Address and Command. Address and Command are transmitted twice. The
second time all bits are inverted and can be used for verification of
the received message. The total transmission time is constant because
every bit is repeated with its inverted length. If you're not interested
in this reliability you can ignore the inverted values, or you can
expand the Address and Command to 16 bits each\!  
Keep in mind that one extra 560µs burst has to follow at the end of the
message in order to be able to determine the value of the last bit.

![](/media/63364daf21e5522c64eb8dfa82f2cef2.png)

A command is transmitted only once, even when the key on the remote
control remains pressed. Every 110ms a repeat code is transmitted for as
long as the key remains down. This repeat code is simply a 9ms AGC pulse
followed by a 2.25ms space and a 560µs burst.

![](/media/afea92a3b5cc1aa2457d2b118b157c84.png)

**Extended NEC protocol:**

The NEC protocol is so widely used that soon all possible addresses were
used up. By sacrificing the address redundancy the address range was
extended from 256 possible values to approximately 65000 different
values. This way the address range was extended from 8 bits to 16 bits
without changing any other property of the protocol.  
By extending the address range this way the total message time is no
longer constant. It now depends on the total number of 1's and 0's in
the message. If you want to keep the total message time constant you'll
have to make sure the number 1's in the address field is 8 (it
automatically means that the number of 0's is also 8). This will reduce
the maximum number of different addresses to just about 13000.

The command redundancy is still preserved. Therefore each address can
still handle 256 different commands.

![](/media/2f78d1ce7f001926f6b90ad966796e91.png)

Keep in mind that 256 address values of the extended protocol are
invalid because they are in fact normal NEC protocol addresses. Whenever
the low byte is the exact inverse of the high byte it is not a valid
extended address.

4. Decoded infrared signal：

We connect the infrared receiving element to the ESP32, according to the
wiring diagram below:

![](/media/700496cb1e0d5d23fd63c28469dd3fd0.png)

**How to add the IRremoteESP8266 library：**

This code uses a library named "**IRremoteESP8266**", if you haven't
installed it yet, please do so before learning. The steps to add
third-party libraries are as follows:

There are two ways to add libraries:

The first way, open the Arduino IDE, click“Sketch”→“Include
Library”→“Manage Libraries...”. Enter“IRremoteESP8266”in the
search box, select“IRremoteESP8266”and click“Update”to install. Please
refer to the following operations :

![](/media/70504b2794644c45ba7d440a79879795.png)

![](/media/71b05cd3f81dae4b7efcf7ffc65920f9.png)

The second way，open the“Sketch”→“Include Library”→“Add .ZIP Library...”.
In the pop-up window, find the file named**“2. Windows System\\2.
C\_Tutorial\\3.Libraries\\IRremoteESP8266-2.7.4.ZIP”**which locates in
this directory. Select the **IRremoteESP8266-2.7.4.ZIP** file，and then
click“Open”.

![](/media/15d3058196199ee96d8e40451d88e8c7.png)

![](/media/91213b8e3ec0a198fcd735ce4db32eed.png)

After the **IRremoteESP8266** library is added, you can open the code we
provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 34：IR Control Sound And
LED\\Project\_34.1\_Decoded\_IR\_Signal”**.

    //**********************************************************************************
    /*  
     * Filename    : Decoded IR Signal
     * Description : Decode the infrared remote control and print it out through the serial port.
     * Auther      : http//www.keyestudio.com
    */
    #include <Arduino.h>
    #include <IRremoteESP8266.h>
    #include <IRrecv.h>
    #include <IRutils.h>
    
    const uint16_t recvPin = 0; // Infrared receiving pin
    IRrecv irrecv(recvPin);      // Create a class object used to receive class
    decode_results results;       // Create a decoding results class object
    
    void setup() {
      Serial.begin(115200);       // Initialize the serial port and set the baud rate to 115200
      irrecv.enableIRIn();        // Start the receiver
      Serial.print("IRrecvDemo is now running and waiting for IR message on Pin ");
      Serial.println(recvPin);   //print the infrared receiving pin
    }
    
    void loop() {
      if (irrecv.decode(&results)) {          // Waiting for decoding
        serialPrintUint64(results.value, HEX);// Print out the decoded results
        Serial.println("");
        irrecv.resume();                      // Release the IRremote. Receive the next value
      }
      delay(1000);
    }
    //**********************************************************************************


Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable, and open the serial monitor and
then set baud rate to 115200. You will see that aim the infrared remote
control transmitter at the infrared receiving head, press the button on
the infrared controller, and the serial port monitor prints the current
received key code values.

![](/media/c8eaa6c1894aaebf907903cc0240bec8.png)

Write down the code associated with each button, because you will need
that information later.

![](/media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

**5. Wiring diagram of the infrared remote control：**

![](/media/4912c1622e0eaedb76ea3a9b8ed969c0.png)

**6. Project code：**

The **IRremoteESP8266** library had been added previously, so you don't
need to add it again. If not, you need to add the **IRremoteESP8266**
library. The steps to add third-party libraries are as shown above.

After the **IRremoteESP8266** library was added, you can open the code
we provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 34：IR Control Sound And
LED\\Project\_34.2\_IR\_Control\_Sound\_And\_LED”**.

    //**********************************************************************************
    /*  
     * Filename    : IR Control Sound And LED
     * Description : Remote control RGB and Passive buzzer with infrared remote control.
     * Auther      : http//www.keyestudio.com
    */
    #include <Arduino.h>
    #include <IRremoteESP8266.h>
    #include <IRrecv.h>
    #include <IRutils.h>
    
    const uint16_t recvPin = 0; // Infrared receiving pin
    IRrecv irrecv(recvPin);      // Create a class object used to receive class
    decode_results results;       // Create a decoding results class object
    
    int ledPins[] = {22, 21, 4};    //define red, green, blue led pins
    const byte chns[] = {0, 1, 2};        //define the pwm channels
    int buzzerPin = 15;  // the number of the buzzer pin
    
    void setup() {
      irrecv.enableIRIn();                  // Start the receiver
      pinMode(buzzerPin, OUTPUT);
      for (int i = 0; i < 3; i++) {   //setup the pwm channels,1KHz,8bit
        ledcSetup(chns[i], 1000, 8);
        ledcAttachPin(ledPins[i], chns[i]);
      }
    }
    
    void loop() {
      if(irrecv.decode(&results)) {        // Waiting for decoding
        handleControl(results.value);       // Handle the commands from remote control
        irrecv.resume();                    // Receive the next value
      }
    }
    
    void handleControl(unsigned long value) {
      // Make a sound when it rereives commands
      digitalWrite(buzzerPin, HIGH);
      delay(100);
      digitalWrite(buzzerPin, LOW);
      // Handle the commands
      if (value == 0xFF6897) // Receive the number '1'
      { 
          ledcWrite(chns[0], 255); //Common cathode LED, high level to turn on the led.
          ledcWrite(chns[1], 0);
          ledcWrite(chns[2], 0);
          delay(1000);
      }
       else if (value == 0xFF9867) // Receive the number '2'
       { 
          ledcWrite(chns[0], 0); 
          ledcWrite(chns[1], 255);
          ledcWrite(chns[2], 0);
          delay(1000);
       }
        else if (value == 0xFFB04F) // Receive the number '3'
       { 
          ledcWrite(chns[0], 0);
          ledcWrite(chns[1], 0);
          ledcWrite(chns[2], 255);
          delay(1000);
        }
        else if (value == 0xFF30CF) // Receive the number '4'
       {  
          ledcWrite(chns[0], 255);
          ledcWrite(chns[1], 255);
          ledcWrite(chns[2], 0);
          delay(1000);
        }
        else if (value == 0xFF18E7) // Receive the number '5'
       {  
          ledcWrite(chns[0], 255);
          ledcWrite(chns[1], 0);
          ledcWrite(chns[2], 255);
          delay(1000);
        }
        else if (value == 0xFF7A85)  // Receive the number '6'
       {  
          ledcWrite(chns[0], 0);
          ledcWrite(chns[1], 255);
          ledcWrite(chns[2], 255);
          delay(1000);
        }
        else if (value == 0xFF10EF)  // Receive the number '7'
       {   
          ledcWrite(chns[0], 255);
          ledcWrite(chns[1], 255);
          ledcWrite(chns[2], 255);
          delay(1000);
        }
        else{
          ledcWrite(chns[0], 0);
          ledcWrite(chns[1], 0);
          ledcWrite(chns[2], 0);
          delay(1000);
          }
      }
    //**********************************************************************************


7. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that press the
1 to 7 key of the infrared remote controller, the buzzer will sound
once, and the RGB light will be red, green, blue, yellow, red, blue,
green and white respectively. Press another key (except 1 to 7 key), and
the RGB light will go off.

(**Note:** Before use, we need to remove the plastic sheet from the
bottom of the infrared remote controller.)

![](/media/3c9d76cb0d24d9861811ce2cb0bb6ae4.png)
