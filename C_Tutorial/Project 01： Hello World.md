# Project 01: Hello World

1. Introduction：

For ESP32 beginners, we'll start with some simple things. In this
project, you just need an ESP32 mainboard, USB cable and computer to
complete“Hello World\!”Project. It is not only a communication test for
ESP32 mainboard and computer, but also a primary project for ESP32.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:1.56875in;height:0.76528in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/3bdcc62cfa661d2b860a76e28537e21e.png" style="width:1.41667in;height:0.76042in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>USB cable*1</td>
</tr>
</tbody>
</table>

3. Wiring：

In this project, we use a USB cable to connect the ESP32 to the
computer.

![](/media/56053f7126905c6def63919c661d5c0a.jpeg)

4. Project code：

You can open the code we provide：

The code used in this project is saved in folder(path :) **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 01：Hello
World\\Project\_01\_Hello\_World”**.

    //*************************************************************************************
    /*
     * Filename    : Hello World
     * Description : Enter the letter R,and the serial port displays"Hello World".
     * Auther      :http//www.keyestudio.com
    */
    char val;// defines variable "val"
    void setup()
    {
    Serial.begin(115200);// sets baudrate to 115200
    }
    void loop()
    {
      if (Serial.available() > 0) {
        val=Serial.read();// reads symbols assigns to "val"
        if(val=='R')// checks input for the letter "R"
        {  // if so,    
         Serial.println("Hello World!");// shows “Hello World !”.
        }
      }
    }
    //*************************************************************************************


Before uploading the project code to ESP32，click“Tools”→“Board” and
select“ESP32 Wrover Module”.

![](/media/c4ddbe3e916fb23b9968cddd6af3ba7a.png)

Select the serial port.

![](/media/ab959184e9e1d0a641945dcf5b8fb945.png)

**Note:** For macOS users, if the uploading fails, please set the baud
rate to 115200 before clicking![](/media/b0d41283bf5ae66d2d5ab45db15331ba.png).

![](/media/46d9ad996b0e750e161cd41cb88ee014.png)

Click![](/media/b0d41283bf5ae66d2d5ab45db15331ba.png)to download the code to ESP32.

![](/media/efed61ebd601af52ee6e5cb66267ea91.png)

**Note:** If uploading the code fails, you can press the Boot button on
ESP32 after click![](/media/d09c4a31563f04a42d451e7bc1a5fb8a.png), and release the Boot
button![](/media/dc77bfcf5851c8f43aab6cbe7cec7920.png) after the percentage of uploading progress
appears, as shown below:

![](/media/157ee2e7687559d9812d24edec758150.png)

The Project code is uploaded successfully！

![](/media/a959a175c20a990a8e68a89825ba4673.png)

5. Project result：

After the project code is uploaded successfully, power up with a USB
cable and click the icon![](/media/2f6bca56f724e45a855335cb53ae9b4e.png)to enter the serial
monitor.

Set baud rate to 115200 and type "R" in the text box. Click "Send", and
the serial monitor will display "Hello World\!”.

![](/media/41f9f3168413965361dd4fa3da54f0ce.png)
