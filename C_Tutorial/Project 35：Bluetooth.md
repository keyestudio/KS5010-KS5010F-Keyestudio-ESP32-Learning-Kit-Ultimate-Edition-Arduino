# Project 35：Bluetooth

This chapter mainly introduces how to make simple data transmission
through bluetooth of ESP32 and mobile phones. Project 35.1 is Classic
Bluetooth and Project 35.2 is Bluetooth Control LED.

**Project 35.1：Classic Bluetooth**

1. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/729232b0c2d2c01984808289b222890c.png" style="width:1.8125in;height:0.86458in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg" style="width:2.43681in;height:1.13472in" /></td>
</tr>
<tr class="even">
<td>USB Cable*1</td>
<td>ESP32*1</td>
</tr>
</tbody>
</table>

In this tutorial we need to use a Bluetooth APP called Serial Bluetooth
Terminal to assist in the experiment. If you've not installed it yet,
please do so by clicking:
<https://www.appsapk.com/serial-bluetooth-terminal/> .The following is
its logo.

![](/media/7b98d6708888b0a6f38f85ffca484857.png)

2. Component knowledge：

ESP32's integrated Bluetooth function Bluetooth is a short-distance
communication system, which can be divided into two types, namely
Bluetooth Low Energy(BLE) and Classic Bluetooth. There are two modes for
simple data transmission: master mode and slave mode.

**Master mode**

In this mode, works are done in the master device and it can connect
with a slave device. And we can search and select slave devices nearby
to connect with. When a device initiates connection request in master
mode, it requires information of the other Bluetooth devices including
their address and pairing passkey. After

finishing pairing, it can connect with them directly.

**Slave mode**

The Bluetooth module in slave mode can only accept connection request
from a host computer, but cannot initiate a connection request. After
connecting with a host device, it can send data to or receive from the
host device.

Bluetooth devices can make data interaction with each other, as one is
in master mode and the other in slave mode. When they are making data
interaction, the Bluetooth device in master mode searches and selects
devices nearby to connect to. When establishing connection, they can
exchange data. When mobile phones

exchange data with ESP32, they are usually in master mode and ESP32 in
slave mode.

![](/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg)

**Master Slave**

3. Wiring Diagram：

We can use a USB cable to connect ESP32 mainboard to the USB port on a
computer.

![](/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg)

4. Project code：

You can open the code we provide:

The code used in this project is saved in folder(path:) **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 35:
Bluetooth\\Project\_35.1\_Classic\_Bluetooth”**.

![](/media/25fad37d4ab57c5ca05f1433b7da3649.png)

    //**********************************************************************************
    /*
     * Filename    : Classic Bluetooth--SerialToSerialBT
     * Description : ESP32 communicates with the phone by bluetooth and print phone's data via a serial port
     * Auther      : http//www.keyestudio.com
    */
    #include "BluetoothSerial.h"
    
    BluetoothSerial SerialBT;
    String buffer;
    void setup() {
      Serial.begin(115200);
      SerialBT.begin("ESP32test"); //Bluetooth device name
      Serial.println("\nThe device started, now you can pair it with bluetooth!");
    }
    
    void loop() {
      if (Serial.available()) {
        SerialBT.write(Serial.read());
      }
      if (SerialBT.available()) {
        Serial.write(SerialBT.read());
      }
      delay(20);
    }
    //**********************************************************************************


**6. Project result:**

Compile and upload the code to the ESP32. After uploading
successfully，we will use a USB cable to power on. Open the serial
monitor and set the baud rate to **115200**. When you see the serial
monitor prints out the character string as below, it indicates that the
Bluetooth of ESP32 is ready and waiting to connect with the mobile
phone. (If open the serial monitor and set the baud rate to 115200, the
information is not displayed, please press the RESET button of the
ESP32)

![](/media/1fd21fafd84d2b529931a89d21a03d6a.png)

![](/media/35c5986d34a01d74bac62e6f6ade7e54.png)

Make sure that the Bluetooth of your phone has been turned on and
“Serial Bluetooth Terminal” has been installed.

![](/media/382529edef3989e60264cad217d88e6f.png)

Click "**Search**" to search Bluetooth devices nearby and select
"**ESP32 test**" to connect to.

![](/media/0608c9a78b5f56d4c8f1994c55c9cd46.png)

Turn on software APP, click the left of the terminal. Select
"**Devices**" .

![](/media/32b8c3abd51fc538ba854b1d72e1165e.png)

Select ESP32test in classic Bluetooth mode, and a successful connecting
prompt will appear as shown on the right illustration.

![](/media/00f9b335cb512704763e3621e7c598b2.png)

And now data can be transferred between your mobile phone and computer
via ESP32.

Send "**Hello\!**" from your phone, when the computer receives it, reply
"**Hi\!**" to your phone.

![](/media/10f1f806f03e3651b3f2779f91aba2fe.png)

![](/media/4f4e6b4e45996ccbde4da17219f02d00.png)

**Project 35.2：Bluetooth Control LED**

1. Components：

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
<td>220ΩResistor*1</td>
<td>Jumper Wires</td>
<td>USB Cable*1</td>
</tr>
</tbody>
</table>

2. Wiring diagram：

![](/media/0735997593c8858ad6441d8e9867206f.png)

3. Project code：

You can open the code we provide：

The code used in this project is saved in folder(path:) **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project
35：Bluetooth\\Project\_35.2\_Bluetooth\_Control\_LED”**.

![](/media/5e2e7ad298202e9e8678d84479d09428.png)

    //**********************************************************************************
    /*
     * Filename    : Bluetooth Control LED
     * Description : The phone controls esp32's led via bluetooth.
                    When the phone sends "LED_on," ESP32's LED lights turn on.
                    When the phone sends "LED_off," ESP32's LED lights turn off.
     * Auther      : http//www.keyestudio.com
    */
    #include "BluetoothSerial.h"
    #include "string.h"
    #define LED 15
    BluetoothSerial SerialBT;
    char buffer[20];
    static int count = 0;
    void setup() {
      pinMode(LED, OUTPUT);
      SerialBT.begin("ESP32test"); //Bluetooth device name
      Serial.begin(115200);
      Serial.println("\nThe device started, now you can pair it with bluetooth!");
    }
    
    void loop() {
      while(SerialBT.available())
      {
        buffer[count] = SerialBT.read();
        count++;
      }
      if(count>0){
        Serial.print(buffer);
        if(strncmp(buffer,"led_on",6)==0){
          digitalWrite(LED,HIGH);
        }
        if(strncmp(buffer,"led_off",7)==0){
          digitalWrite(LED,LOW);
        }
        count=0;
        memset(buffer,0,20);
      }
    }
    //**********************************************************************************


**4. Project result：**

Compile and upload the code to the ESP32, after uploading
successfully，we will use a USB cable to power on. The operation of the
APP is the same as Project 35.1, you only need to change the sending
content to “LED on"and “LED off” to operate LEDs on the ESP32. Data sent
from mobile APP:

![](/media/21ec63e3abe43a119ab8a3d4634894f0.png)

Display on the serial port of the computer:

![](/media/f5d5d544d23177674a0b206254fa645b.png)

The phenomenon of LED：

![](/media/a1e66d46e5797995a1b66a761c7857f8.png)

**Attention:** If the sending content isn't “led-on”or “led-off”, then
the state of LED will not change. If the LED is on, when receiving
irrelevant content, it keeps on; Correspondingly, if the LED is off,
when receiving irrelevant content, it keeps off.
