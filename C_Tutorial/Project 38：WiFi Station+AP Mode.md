# Project 38：WiFi Station+AP Mode

1. Introduction：

ESP32 has three different WiFi operating modes : Station mode，AP
mode and AP+Station mode. All WiFi programming projects must be
configured with WiFi operating mode before using WiFi, otherwise
WiFi cannot be used. In this project, we will learn ESP32's WiFi
Station+AP mode.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/729232b0c2d2c01984808289b222890c.png" style="width:1.8125in;height:0.86458in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg" style="width:2.43681in;height:1.13472in" /></td>
</tr>
<tr class="even">
<td> USB Cable*1</td>
<td>ESP32*1</td>
</tr>
</tbody>
</table>

3. Wiring：

Connect the ESP32 to the USB port on your computer using a USB cable.

![](/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg)

4. Component knowledge：

**AP+Station mode:** In addition to AP mode and Station mode, ESP32 can
also use AP mode and Station mode at the same time. This mode contains
the functions of the previous two modes. Turn on ESP32's Station mode,
connect it to the router network, and it can communicate with the
Internet via the router. At the same time, turn on its AP mode to create
a hotspot network. Other WiFi devices can choose to connect to the
router network or the hotspot network to communicate with ESP32.

5. Project code：

You can open the code we provide：

The code used in this project is saved in folder(path:) **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 38：WiFi Station+AP
Mode\\Project\_38\_WiFi\_Station\_AP\_Mode”**.

![](/media/35c5a68c7ac336892d89e2bd7c480d23.png)

It is analogous to Project 36 and Project 37. Before running the code,
you need to modify ssid\_Router, password\_Router, ssid\_AP and
password\_AP shown in the box of the illustration above.

![](/media/ba6aea8a6755907ac8d53132278669d1.png)

    //**********************************************************************************
    /*
     * Filename    : WiFi AP+Station
     * Description : ESP32 connects to the user's router, turning on an access point
     * Auther      : http//www.keyestudio.com
    */
    #include <WiFi.h>
     
    const char *ssid_Router     =  "ChinaNet-2.4G-0DF0";  //Enter the router name
    const char *password_Router =  "ChinaNet@233";  //Enter the router password
    const char *ssid_AP         =  "ESP32_WiFi"; //Enter the router name
    const char *password_AP     =  "12345678";  //Enter the router password
    
    void setup(){
      Serial.begin(115200);
      Serial.println("Setting soft-AP configuration ... ");
      WiFi.disconnect();
      WiFi.mode(WIFI_AP);
      Serial.println("Setting soft-AP ... ");
      boolean result = WiFi.softAP(ssid_AP, password_AP);
      if(result){
        Serial.println("Ready");
        Serial.println(String("Soft-AP IP address = ") + WiFi.softAPIP().toString());
        Serial.println(String("MAC address = ") + WiFi.softAPmacAddress().c_str());
      }else{
        Serial.println("Failed!");
      }
      
      Serial.println("\nSetting Station configuration ... ");
      WiFi.begin(ssid_Router, password_Router);
      Serial.println(String("Connecting to ")+ ssid_Router);
      while (WiFi.status() != WL_CONNECTED){
        delay(500);
        Serial.print(".");
      }
      Serial.println("\nConnected, IP address: ");
      Serial.println(WiFi.localIP());
      Serial.println("Setup End");
    }
    
    void loop() {
    }
    //**********************************************************************************


6. Project result：

After making sure that the code is modified correctly, compile and
upload the code to ESP32, open the serial monitor and set baud rate to
115200. And then it will display as follows: (If open the serial monitor
and set the baud rate to 115200, the information is not displayed,
please press the RESET button of the ESP32)

![](/media/1fd21fafd84d2b529931a89d21a03d6a.png)

![](/media/68aa510490b2ef48ec0ac087d1b763a9.png)

When observing the print information of the serial monitor, turn on the
WiFi scanning function of your phone, and you can see the ssid\_AP on
ESP32.

![](/media/3e0ad895bea7f5100cc02a415adcace7.png)
