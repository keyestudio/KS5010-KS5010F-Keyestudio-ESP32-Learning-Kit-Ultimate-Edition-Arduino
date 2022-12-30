# Project 36：WiFi Station Mode

1. Introduction：

ESP32 has three different WiFi operating modes : Station mode，AP mode
and AP+Station mode. All WiFi programming projects must be configured
with WiFi operating mode before using WiFi, otherwise WiFi cannot be
used. In this project, we will learn about ESP32's WiFi Station mode.

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

Connect the ESP32 to the USB port on your computer using a USB cable.

![](/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg)

4. Component knowledge：

**Station mode:** When ESP32 selects Station mode, it acts as a WiFi
client. It can connect to the router network and communicate with other
devices on the router via WiFi connection. As shown below, the PC is
connected to the router, and if ESP32 wants to communicate with the PC,
it needs to be connected to the router.

![](/media/f74baff97695aa2ee33a8c19370d2547.png)

5. Project code：

You can open the code we provide：

The code used in this project is saved in folder(path:) **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 36：WiFi Station
Mode\\Project\_36\_WiFi\_Station\_Mode”**.

![](/media/f9fca49fbf789a07bb04ab0701a53937.png)

Because the names and passwords of routers in various places are
different, before the code runs, users need to enter the correct
router’s name and password in the box as shown in the illustration
above.

![](/media/5205db683644772e9df6ba0f391f4b43.png)

    //**********************************************************************************
    /*
     * Filename    : WiFi Station
     * Description : Connect to your router using ESP32
     * Auther      : http//www.keyestudio.com
    */
    #include <WiFi.h> //Include the WiFi Library header file of ESP32.
    
    //Enter correct router name and password.
    const char *ssid_Router     = "ChinaNet-2.4G-0DF0"; //Enter the router name
    const char *password_Router = "ChinaNet@233"; //Enter the router password
    
    void setup(){
      Serial.begin(115200);
      delay(2000);
      Serial.println("Setup start");
      WiFi.begin(ssid_Router, password_Router);//Set ESP32 in Station mode and connect it to your router.
      Serial.println(String("Connecting to ")+ssid_Router);
    //Check whether ESP32 has connected to router successfully every 0.5s.  
      while (WiFi.status() != WL_CONNECTED){
        delay(500);
        Serial.print(".");
      }
      Serial.println("\nConnected, IP address: ");
      Serial.println(WiFi.localIP());//Serial monitor prints out the IP address assigned to ESP32.
      Serial.println("Setup End");
    }
     
    void loop() {
    }
    //**********************************************************************************


6. Project result：

After making sure the router name and password are entered correctly,
compile and upload the code to ESP32, open serial monitor and set baud
rate to 115200. When ESP32 successfully connects to “ssid\_Router”,
serial monitor will print out the IP address assigned to ESP32 by the
router. (If open the serial monitor and set the baud rate to 115200, the
information is not displayed, please press the RESET button of the
ESP32)

![](/media/1fd21fafd84d2b529931a89d21a03d6a.png)

![](/media/efc6081aa00e0ce19df5501de76482da.png)
