# Project 37：WiFi AP Mode

1. Introduction：

ESP32 has three different WiFi operating modes : Station mode，AP
mode and AP+Station mode. All WiFi programming projects must be
configured with WiFi operating mode before using WiFi, otherwise
WiFi cannot be used. In this project, we will learn about ESP32's
WiFi AP mode.

2. Components：

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

3. Wiring：

Connect the ESP32 to the USB port on your computer using a USB
cable.

![](/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg)

4. Component knowledge：

**AP mode :** When ESP32 selects AP mode, it creates a hotspot network
that is separated from the Internet and waits for other WiFi devices to
connect. As shown in the figure below, ESP32 is used as a hotspot. If a
mobile phone or PC wants to communicate with ESP32, it must be connected
to the hotspot of ESP32. Only after a connection is established with
ESP32 can they communicate.

![](/media/35d90f1ce10814ea1897ba63f8bd7ad9.png)

5. Project code：

You can open the code we provide：

The code used in this project is saved in folder(path:) **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 37：WiFi AP
Mode\\Project\_37\_WiFi\_AP\_Mode”**.

![](/media/d68424e3ba30f3a50feab1d9864a8beb.png)

Before the code runs, you can make any changes to the AP name and
password for ESP32 in the box as shown in the illustration above. Of
course, you can leave it alone by default.

![](/media/b83d79a6be47aac434c526e80922a0a4.png)

    //**********************************************************************************
    /*
     * Filename    : WiFi AP
     * Description : Set ESP32 to open an access point
     * Auther      : http//www.keyestudio.com
    */
    #include <WiFi.h> //Include the WiFi Library header file of ESP32.
    
    const char *ssid_AP     = "ESP32_WiFi"; //Enter the router name
    const char *password_AP = "12345678"; //Enter the router password
    
    IPAddress local_IP(192,168,1,108);//Set the IP address of ESP32 itself
    IPAddress gateway(192,168,1,1);   //Set the gateway of ESP32 itself
    IPAddress subnet(255,255,255,0);  //Set the subnet mask for ESP32 itself
    
    void setup(){
      Serial.begin(115200);
      delay(2000);
      Serial.println("Setting soft-AP configuration ... ");
      WiFi.disconnect();
      WiFi.mode(WIFI_AP);
      Serial.println(WiFi.softAPConfig(local_IP, gateway, subnet) ? "Ready" : "Failed!");
      Serial.println("Setting soft-AP ... ");
      boolean result = WiFi.softAP(ssid_AP, password_AP);
      if(result){
        Serial.println("Ready");
        Serial.println(String("Soft-AP IP address = ") + WiFi.softAPIP().toString());
        Serial.println(String("MAC address = ") + WiFi.softAPmacAddress().c_str());
      }else{
        Serial.println("Failed!");
      }
      Serial.println("Setup End");
    }
     
    void loop() {
    }
    //**********************************************************************************


6. Project result：

Enter the ESP32 AP name and password correctly, compile and upload the
code to ESP32, open the serial monitor and set the baud rate to
**115200**. And then it will display as follows.

(If open the serial monitor and set the baud rate to 115200, the
information is not displayed, please press the RESET button of the
ESP32)

![](/media/1fd21fafd84d2b529931a89d21a03d6a.png)

![](/media/12f1c45c84266573c43bd7a7cda826a5.png)

When observing the print information of the serial monitor, turn on the
WiFi scanning function of your phone, and you can see the ssid\_AP on
ESP32, which is called "ESP32\_Wifi" in this Code. You can enter the
password "12345678" to connect it or change its AP name and password by
modifying Code.

![](/media/3e0ad895bea7f5100cc02a415adcace7.png)
