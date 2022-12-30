# Project 40：WiFi Smart Home

1. Introduction：

In the previous experiment, we have learned the WiFi Station mode, WiFi
AP mode and WiFi AP+Station mode of the ESP32. In this project, we will
use ESP32's WiFi Station mode to control the work of multiple
sensors/modules through APP connection with WiFi to achieve the effect
of WiFi smart home.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/f4be217034b7f60027b51e90b55adf95.png" style="width:1.05278in;height:0.48819in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.54861in;height:1.34583in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/4dc1472ab8d2cf85fd7518646e10d0ee.png" style="width:1.16944in;height:0.5in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/8a6ed6668f0d1812d09dd361388ae087.png" style="width:1.05694in;height:0.57292in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/1886ee7e1faeea2c093ae626e1b8baaf.png" style="width:1.05764in;height:0.82014in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>130 Motor*1</td>
<td>5V Relay Module*1</td>
<td>Servo*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/ba1d8f61328a0e474b423e826279dbb7.png" style="width:0.88472in;height:0.66875in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/85df6831220dec7d43a68bfc9b7382cb.png" style="width:1.325in;height:0.87569in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/279bc43f67dbfe97a4ab19082a29fc5d.png" style="width:0.97083in;height:0.81042in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e3cf4510b86b7e0fd5b2880cd433cc25.png" style="width:0.40278in;height:0.80347in" /><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/c607c1042325f6c2fa3db027e8611351.png" style="width:0.84236in;height:0.50139in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e9a8d050105397bb183512fb4ffdd2f6.png" style="width:0.90694in;height:0.90139in" /></td>
</tr>
<tr class="even">
<td>Temperature and Humidity Sensor*1</td>
<td>HC-SR04 Ultrasonic Sensor*1</td>
<td>M-F Dupont Wires</td>
<td>Smartphone/Tablet*1</td>
<td>Jumper Wires</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/559e43bc8a25731e5be966c02d6798e6.jpeg" style="width:1.14514in;height:0.82708in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/a815c48437199c6ab79d74cd2d583de0.png" style="width:0.28125in;height:1.29792in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/0617c92e06f8ca1ebeaca24bdf692875.png" style="width:1.07361in;height:0.42778in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/412d874475de346d56b39cfb041ffc4c.png" style="width:1.19167in;height:0.51458in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/009965e315276ecf1144c22c54a93fd9.png" style="width:0.94375in;height:0.82986in" /></td>
</tr>
<tr class="even">
<td>Battery Holder*1</td>
<td>Battery(self-provided)*6</td>
<td>USB Cable*1</td>
<td>Keyestudio breadboard special power module*1</td>
<td>Fan*1</td>
</tr>
</tbody>
</table>

3. Wiring diagram：

<table>
<tbody>
<tr class="odd">
<td>Relay Module</td>
<td>ESP32</td>
<td></td>
<td>Temperature and Humidity Sensor</td>
<td>ESP32</td>
</tr>
<tr class="even">
<td>G</td>
<td>G</td>
<td></td>
<td>G</td>
<td>G</td>
</tr>
<tr class="odd">
<td>V</td>
<td>5V</td>
<td></td>
<td>V</td>
<td>3V3</td>
</tr>
<tr class="even">
<td>S</td>
<td>IO32</td>
<td></td>
<td>S</td>
<td>IO15</td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Ultrasonic Sensor</td>
<td>ESP32</td>
<td></td>
<td>130 Motor</td>
<td>ESP32</td>
</tr>
<tr class="odd">
<td>Vcc</td>
<td>5V</td>
<td></td>
<td>G</td>
<td>G</td>
</tr>
<tr class="even">
<td>Trig</td>
<td>IO14</td>
<td></td>
<td>V</td>
<td>5V</td>
</tr>
<tr class="odd">
<td>Echo</td>
<td>IO27</td>
<td></td>
<td>IN+</td>
<td>IO19</td>
</tr>
<tr class="even">
<td>Gnd</td>
<td>G</td>
<td></td>
<td>IN-</td>
<td>IO18</td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Servo</td>
<td>ESP32</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Red line</td>
<td>5V</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Brown line</td>
<td>G</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Orange line</td>
<td>IO4</td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

![](/media/fd7a7efd4bc365e1524011b68217dee5.png)

(Note: Connect the wires and then install a small fan blade on the DC
motor. )

4. Install APP:

Android system (Smartphone/Tablet) APP:

We provide the Android APP installation package：

![](/media/c8d89f132571775e82a6fedbd075200c.png)

**Installation steps：**

Now transfer the **keyes wifi.apk** file in the folder to android phone
or tablet, click **keyes wifi.apk** file to enter the installation page,
click“ALLOW”, then click“INSTALL”, after a while, click“OPEN”after the
installation is completed to enter the APP interface.

![](/media/c8d89f132571775e82a6fedbd075200c.png)

![](/media/d620452a9d6188cb3946269510df5ae0.png)

![](/media/b311329042f5bbd2880841127b91ebf8.png)

![](/media/7c5cfc935371c8e2ab30e999775d5f8f.png)

![](/media/d48c065ebaf1c5ca652eb72b15d3e596.png)

![](/media/78c89b91c0af2268f6267813e7923a9b.png)

IOS system (Smartphone/Tablet) APP:

a.Open App Store.

![](/media/27924fdb3d67692df7c63d8d0fb72287.png)

b. Enter keyes link in the search box and click Search. The download
interface appears. Click“![](/media/962a57f92b78eea1f0e3e81463497a9c.png)”to download and install
the APP of keyes link. The following operations are similar to those of
Android system, you can refer to the steps of Android system above for
operation.

5. Add the xht11 and ESP32Servo libraries：

This code uses two libraries named "**xht11**" and "**ESP32Servo**" , if
you haven't installed them yet, please do so before learning. The steps
to add third-party libraries are as follows:

Add the xht11 library first:

Open the Arduino IDE，click“Sketch”→“Include Library”→“Add .zip
Library...”. In the pop-up window, find the file named **“2 Windows
System\\2. C\_Tutorial\\3.Libraries\\xht11.ZIP”** which locates in this
directory. Select the **xht11.ZIP** file and then click“Open”.

![](/media/bafc269b425a978bd50846391d53da8a.png)

![](/media/e6d2e9f9b575f99bf4194a620f1b5dc3.png)

Then Add the ESP32Servo library:

Open the Arduino IDE，click “Sketch”→“Include Library”→“Add .ZIP
Library...”. In the pop-up window, find the file named**“2. Windows
System\\2. C\_Tutorial\\3.Libraries\\ESP32Servo-0.8.0.ZIP”**which
locates in this directory. Select the **ESP32Servo-0.80.ZIP** file，and
then click“Open”.

![](/media/bafc269b425a978bd50846391d53da8a.png)

![](/media/f5db0a244df656b0fd9b2d5b8d42c1a5.png)

6. Project code：

After the **xht11** and **ESP32Servo** libraries were added, you can
open the code we provide：

The code used in this project is saved in folder(path:) **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 40：WiFi Smart
Home\\Project\_40\_WiFi\_Smart\_Home”**.

    //**********************************************************************************
    /*  
     * Filename    : WiFi Smart Home.
     * Description : WiFi APP controls Multiple sensors/modules work to achieve the effect of WiFi smart home.
     * Auther      : http//www.keyestudio.com
    */
    #include <Arduino.h>
    #include <WiFi.h>
    #include <ESPmDNS.h>
    #include <WiFiClient.h>
    
    #include "xht11.h"
    //gpio15
    xht11 xht(15);
    unsigned char dht[4] = {0, 0, 0, 0};
    
    #include <ESP32Servo.h>
    Servo myservo;
    int servoPin = 4;
    #define Relay  32
    #define IN1 19  //IN1 corresponds to IN+
    #define IN2 18 //IN2 corresponds to IN-
    #define trigPin  14
    #define echoPin  27
    
    int distance1;
    String dis_str;
    int ip_flag = 1;
    int ultra_state = 1;
    int temp_state = 1;
    int humidity_state = 1;
    
    String item = "0";
    const char* ssid = "ChinaNet-2.4G-0DF0"; //the name of user's wifi
    const char* password = "ChinaNet@233";  //the password of user's wifi
    WiFiServer server(80);
    String unoData = "";
    
    void setup() {
      Serial.begin(115200);
      pinMode(Relay, OUTPUT);
      myservo.setPeriodHertz(50);   
      myservo.attach(servoPin, 500, 2500);
      pinMode(IN1, OUTPUT);
      pinMode(IN2, OUTPUT);
      
      WiFi.begin(ssid, password);
      while (WiFi.status() != WL_CONNECTED) {
        delay(500);
        Serial.print(".");
      }
      Serial.println("");
      Serial.print("Connected to ");
      Serial.println(ssid);
      Serial.print("IP address: ");
      Serial.println(WiFi.localIP());
      server.begin();
      Serial.println("TCP server started");
      MDNS.addService("http", "tcp", 80);
    
      digitalWrite(IN1, LOW);
      digitalWrite(IN2, LOW);
      digitalWrite(Relay, LOW);
      pinMode(trigPin, OUTPUT);
      pinMode(echoPin, INPUT);
    }
    
    void loop() {
      WiFiClient client = server.available();
      if (!client) {
          return;
      }
      while(client.connected() && !client.available()){
          delay(1);
      }
      String req = client.readStringUntil('\r');
      int addr_start = req.indexOf(' ');
      int addr_end = req.indexOf(' ', addr_start + 1);
      if (addr_start == -1 || addr_end == -1) {
          Serial.print("Invalid request: ");
          Serial.println(req);
          return;
      }
      req = req.substring(addr_start + 1, addr_end);
      item=req;
      Serial.println(item);
      String s;
      if (req == "/")
      {
          IPAddress ip = WiFi.localIP();
          String ipStr = String(ip[0]) + '.' + String(ip[1]) + '.' + String(ip[2]) + '.' + String(ip[3]);
          s = "HTTP/1.1 200 OK\r\nContent-Type: text/html\r\n\r\n<!DOCTYPE HTML>\r\n<html>Hello from ESP32 at ";
          s += ipStr;
          s += "</html>\r\n\r\n";
          Serial.println("Sending 200");
          client.println(s);
      }
      else if(req == "/btn/0")
      {
        Serial.write('a');
        client.println(F("turn on the relay"));
        digitalWrite(Relay, HIGH);
      }
      else if(req == "/btn/1")
      {
        Serial.write('b');
        client.println(F("turn off the relay"));
        digitalWrite(Relay, LOW);
      }
      else if(req == "/btn/2")
      {
        Serial.write('c');
        client.println("Bring the steering gear over 180 degrees");
        myservo.write(180); 
        delay(200);
      }
      else if(req == "/btn/3")
      {
        Serial.write('d');
        client.println("Bring the steering gear over 0 degrees");
        myservo.write(0); 
        delay(200);
      }
      else if(req == "/btn/4")
      {
        Serial.write('e');
        client.println("esp32 already turn on the fans");
        digitalWrite(IN1, LOW); 
        digitalWrite(IN2, HIGH);
      }
      else if(req == "/btn/5")
      {
        Serial.write('f');
        client.println("esp32 already turn off the fans");
        digitalWrite(IN1, LOW); 
        digitalWrite(IN2, LOW);
      }
      else if(req == "/btn/6")
      {
        Serial.write('g');
        while(Serial.available() > 0)
        {
          unoData = Serial.readStringUntil('#');
          client.println("Data");
        }
        while(ultra_state>0)
           {
              Serial.print("Distance = "); 
              Serial.print(checkdistance());
              Serial.println("#");
              Serial1.print("Distance = "); 
              Serial1.print(checkdistance());
              Serial1.println("#");  
              int t_val1 = checkdistance();
              client.print("Distance(cm) = ");
              client.println(t_val1); 
              ultra_state = 0;
            }
      }
      else if(req == "/btn/7")
      {
        Serial.write('h');
        client.println("turn off the ultrasonic");
        ultra_state = 1;
      }
      else if(req == "/btn/8")
      {
        Serial.write('i');
        while(Serial.available() > 0)
         {
          unoData = Serial.readStringUntil('#');
          client.println(unoData);
         }
        while(temp_state>0)
          {
            if (xht.receive(dht)) {
              Serial.print("Temperature = "); 
              Serial.print(dht[2],1);
              Serial.println("#");
              Serial1.print("Temperature = "); 
              Serial1.print(dht[2],1);
              Serial1.println("#");
              int t_val2 = dht[2];
              client.print("Temperature(℃) = ");
              client.println(t_val2);
            }
            temp_state = 0;
          }
      }
      else if(req == "/btn/9")
      {
        Serial.write('j');
        client.println("turn off the temperature");
        temp_state = 1;
      }
      else if(req == "/btn/10")
      {
        Serial.write('k');
        while(Serial.available() > 0)
         {
           unoData = Serial.readStringUntil('#');
           client.println(unoData);
         }
        while(humidity_state > 0)
          {
            if (xht.receive(dht)) {
              Serial.print("Humidity = "); 
              Serial.print(dht[0],1);
              Serial.println("#");
              Serial1.print("Humidity = "); 
              Serial1.print(dht[0],1);
              Serial1.println("#");
              int t_val3 = dht[0];
              client.print("Humidity(%) = ");
              client.println(t_val3);
            }
            humidity_state = 0;
          }
      }
      else if(req == "/btn/11")
      {
        Serial.write('l');
        client.println("turn off the humidity");
        humidity_state = 1;
        }
      //client.print(s);
      client.stop();
    }
    
    int checkdistance() {
      digitalWrite(14, LOW);
      delayMicroseconds(2);
      digitalWrite(14, HIGH);
      delayMicroseconds(10);
      digitalWrite(14, LOW);
      int distance = pulseIn(27, HIGH) / 58;
      
      delay(10);
      return distance;
    }
    //**********************************************************************************


**Special attention:** you need to change the user's Wifi name and Wifi
password in the experiment code to your own Wifi name and Wifi password.

![](/media/9ddee42d7e41abd8a6db60d447cd9f68.png)

7. Project result：

After making sure that the Code is modified correctly, external power
supply and power on, and then compile and upload the code to
ESP32.（**Note:** If uploading the code fails, you can press the Boot
button on ESP32 after click![](/media/d09c4a31563f04a42d451e7bc1a5fb8a.png), and release the Boot
button![](/media/dc77bfcf5851c8f43aab6cbe7cec7920.png) after the percentage of uploading progress
appears），open the serial monitor and set baud rate to 115200. In this
way, the serial port monitor prints the detected WiFi IP address,(If
open the serial monitor and set the baud rate to 115200, the information
is not displayed, please press the RESET button of the ESP32)

![](/media/1fd21fafd84d2b529931a89d21a03d6a.png)

![](/media/ffef6aa96cc6bb3949a735ddc9b91128.png)

Then open the WiFi APP and enter the detected WiFi IP address in the
text box in front of the WiFi button (for example, the IP address shown
by the serial port monitor below :192.168.0.156), then click the WiFi
button, “Hello from ESP32 at 192.168.0.156”is displayed in the text box
next to the WiFi IP address, indicating that the APP is already
connected to WiFi.(WiFi IP address sometimes changes, if the original IP
address doesn't work, you need to re-check the WiFi IP address)

![](/media/ac1bd20a153c3abc5c0c62a416446f52.jpeg)

After the APP has been connected to WiFi, the following operations will
be performed:

1)  Click![](/media/5b9754cb6ec4f995c9eada1da89a8969.png)button, the relay will be opened, the
APP will display![](/media/505b00b0e23f6498c5d51d5d775c8fcb.png)，and the indicator lights up
on the module. Click![](/media/5b9754cb6ec4f995c9eada1da89a8969.png)again, the relay will be
closed, the APP will display ![](/media/deb54a77cdcc87d7569e8b8e46de129f.png)，and the
indicator on the module is off.

2)  Click![](/media/c54f78d819d4e6a8310eaeb79ff66910.png)button，the servo rotates 180°，the APP
will display
![](/media/c54f78d819d4e6a8310eaeb79ff66910.png)again，the APP
will display ![](/media/dee12bee3866542bfe5d70a539f79f0b.png)，the servo rotates 0°.

3)  Click![](/media/5490abf5b2f8a1d9cea3055da07c251c.png)button，the motor（with small fan
blades）rotates，the APP will display
![](/media/5490abf5b2f8a1d9cea3055da07c251c.png)again，close
the motor，the APP will display ![](/media/de6da02ede6d63344546173d36bf5371.png)；

4)  Click![](/media/95bfbe879d2391e4e48dcae085abe5a6.png)button，the ultrasonic sensor detects the
distance, put an object in front of the ultrasonic sensor, the APP
will display

![](/media/e431e1b9c95bed37b053ae9617f93676.png)（different distances show different numbers）,
the distance between the object and the ultrasonic sensor is
6cm；click ![](/media/95bfbe879d2391e4e48dcae085abe5a6.png) again, turn off the sensor, the
APP will display ![](/media/b1df35af68601022e54b7e575b0a07c7.png).

5)  Click![](/media/08c8a35841b31fa4b5327fb7b23a7af5.png)button，the temperature and humidity
sensor measures the temperature in the environment, the APP will
display ![](/media/0aafd0af43f80b692eca3d6732b551b2.png)（different temperatures show
different temperature values），the ambient temperature is 30°C.,
click![](/media/08c8a35841b31fa4b5327fb7b23a7af5.png) again, turn off the sensor，the APP will
display ![](/media/82887a1385bc7411ecbdc41f60ebd450.png).

6)  Click ![](/media/d8e3463ab2f644b3300cdeaa2a68e4c2.png) button，the temperature and humidity
sensor measures the humidity in the environment,，the APP will
display ![](/media/320b86323631e095db330a22ca97bad7.png)（different humiditys show different
humiditys values）, the ambient humidity is
55%；click![](/media/d8e3463ab2f644b3300cdeaa2a68e4c2.png)again，turn off the sensor, the APP
will display ![](/media/adc18d06e626af067286da9040c20252.png).
