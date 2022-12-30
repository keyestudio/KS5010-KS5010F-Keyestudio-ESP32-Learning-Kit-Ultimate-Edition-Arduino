# Project 33：Keypad Door

1. Introduction：

Commonly used digital button sensor, one button uses an IO port.
However, it will occupy too many IO ports when we need a lot of
buttons. In order to save the use of IO ports, the multiple buttons
are made into a matrix type, through the control of the line and row
to achieve less IO port control of multiple buttons. In this
project, we will learn ESP32 and thin film 4\*4 matrix keyboard
control a servo and a buzzer.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/56053f7126905c6def63919c661d5c0a.jpeg" style="width:1.59722in;height:0.77986in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.68056in;height:1.66944in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/cd0bc424e9916881a1a903793821a042.png" style="width:1.25417in;height:1.04792in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/4b4f653a76a82a3b413855493cc58fba.png" style="width:0.86111in;height:0.70069in" /></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>Servo*1</td>
<td>Active Buzzer*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/fcd187eb009098d691927511606c991b.jpeg" style="width:1.70972in;height:0.74931in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e9a8d050105397bb183512fb4ffdd2f6.png" style="width:0.90694in;height:0.90139in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:0.99028in;height:0.52986in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/098a2730d0b0a2a4b2079e0fc87fd38b.png" style="width:0.90833in;height:0.23681in" /></td>
</tr>
<tr class="even">
<td>4*4 Membrane Matrix Keyboard*1</td>
<td>Jumper Wires</td>
<td>USB Cable*1</td>
<td>1kΩResistor*1</td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/9197d4aff9356c585b7ef68e33a6881d.png" style="width:0.27986in;height:1.08819in" /></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>NPN transistor(S8050)*1</td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

3. Component knowledge：

**4\*4 Matrix keyboard：**A Keypad Matrix is a device that integrates a
number of keys in one package. As is shown below, a 4x4 Keypad Matrix
integrates 16 keys:

![](/media/fcd187eb009098d691927511606c991b.jpeg)

Similar to the integration of an LED Matrix, the 4x4 Keypad Matrix has
each row of keys connected with one pin and this is the same for the
columns. Such efficient connections reduce the number of processor ports
required. The internal circuit of the Keypad Matrix is shown below.

![](/media/5ebdacba906622079e0ef41dc1ea3fdf.png)

The method of usage is similar to the Matrix LED, by using a row or
column scanning method to detect the state of each key’s position by
column and row. Take column scanning method as an example, send low
level to the first 4 column (Pin4), detect level state of row 1, 2, 3, 4
to judge whether the key A, B, C, D are pressed. Then send low level to
column3, 2, 1 in turn to detect whether other keys are pressed. By this
means, you can get the state of all of the keys.

4. Read the key value of the 4\*4 matrix keyboard：

We start with a simple code to read the values of the 4\*4 matrix
keyboard and print them in the serial monitor. Its wiring diagram is
shown below：

![](/media/8bfa0e1b1a0f53598f51341d51bc7601.png)

**How to add the Keypad library：**

This code uses a library named "**Keypad**", if you haven't installed it
yet, please do so before learning. The steps to add third-party
libraries are as follows:

There are two ways to add libraries:

The first way, open the Arduino IDE, click“Sketch”→“Include
Library”→“Manage Libraries...”. Enter“Keypad”in the search box,
select“Keypad”and click“Update”to install. Please refer to the following
operations :

![](/media/923515e12b3de3743204ae217f5b051f.png)

![](/media/4b6e1251a79e68ec7f3bbc512ba7fbdd.png)

The second way，open the Arduino IDE，click “Sketch”→“Include
Library”→“Add .ZIP Library...”. In the pop-up window, find the
file named**“2. Windows System\\****2.
C\_Tutorial\\3.Libraries\\****Keypad-3.1.1.ZIP”**which locates in this
directory. Select the **Keypad-3.1.1.ZIP** file，and then click“Open”.

![](/media/59ad80016abb0ea494f3209d0d0889eb.png)

![](/media/d8b183cc743b084df17ec0092ced8191.png)

After the **Keypad** library is added, you can open the code we provide：

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project
3 **”.

    //**********************************************************************************
    /*  
     * Filename    : 4x4 Matrix Keypad Display 
     * Description : Get the value for the matrix keyboard
     * Auther      : http//www.keyestudio.com
    */
    #include <Keypad.h>
    
    // define the symbols on the buttons of the keypad
    char keys[4][4] = {
      {'1', '2', '3', 'A'},
      {'4', '5', '6', 'B'},
      {'7', '8', '9', 'C'},
      {'*', '0', '#', 'D'}
    };
    
    byte rowPins[4] = {22, 21, 19, 18}; // connect to the row pinouts of the keypad
    byte colPins[4] = {17, 16, 4, 0};   // connect to the column pinouts of the keypad
    
    // initialize an instance of class NewKeypad
    Keypad myKeypad = Keypad(makeKeymap(keys), rowPins, colPins, 4, 4);
    
    void setup() {
      Serial.begin(115200); // Initialize the serial port and set the baud rate to 115200
      Serial.println("ESP32 is ready!");  // Print the string "UNO is ready!"
    }
    
    void loop() {
      // Get the character input
      char keyPressed = myKeypad.getKey();
      // If there is a character input, sent it to the serial port
      if (keyPressed) {
        Serial.println(keyPressed);
      }
    }
    //**********************************************************************************


Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable, and open the serial monitor and
then set baud rate to 115200. You will see that press the keyboard and
the serial port monitor prints the corresponding key value, as shown
below.

![](/media/a35e94a442c20325472043ab62589258.png)

5. Wiring diagram of the Keypad Door：

In the last experiment, we have known the key values of the 4\*4 matrix
keyboard. Next, we use it as the keyboard to control a servo and a
buzzer.

![](/media/862e840117a46c1174522a734e28e2f0.png)

6. Adding the Keypad and ESP32Servo** **libraries：

The **Keypad** and **ESP32Servo** libraries had been added
previously, so you don't need to add them again. If not, you need to
add **Keypad** and **ESP32Servo** libraries. The steps to add
third-party Libraries are as follows:

First, add the **ESP32Servo** library：

Open the Arduino IDE，click“Sketch”→“Include Library”→“Add .ZIP
Library...”. In the pop-up window, find the file named **“2. Windows
System\\2. C\_Tutorial\\3.Libraries\\ESP32Servo-0.8.0.ZIP”** which
locates in this directory. Select the **ESP32Servo-0.80.ZIP** file and
then click“Open”.

![](/media/710e5782c37ff2a65ddde368470ce1c5.png)

![](/media/7821c38a6056ac77c2917080e9f557b1.png)

Then, add the **Keypad** library：

Open the Arduino IDE，click “Sketch”→“Include Library”→“Add .ZIP
Library...”. In the pop-up window, find the file named **“2. Windows
System\\2. C\_Tutorial\\3.Libraries\\Keypad-3.1.1.ZIP”** which locates
in this directory. Select the **Keypad-3.1.1.ZIP** file and then
click“Open”.

![](/media/710e5782c37ff2a65ddde368470ce1c5.png)

![](/media/d8b183cc743b084df17ec0092ced8191.png)

7. Project code：

After the **Keypad** and **ESP32Servo** libraries were added, you can
open the code we provide：

The code used in this project is saved in folder **“2. Windows
System\\****2. C\_Tutorial\\2. Projects\\Project 33：Keypad
Door\\Project\_33.2\_Keypad\_Door”**.

    //**********************************************************************************
    /*  
     * Filename    : Keypad_Door
     * Description : Make a simple combination lock.
     * Auther      : http//www.keyestudio.com
    */
    #include <Keypad.h>
    #include <ESP32Servo.h>
    
    // define the symbols on the buttons of the keypad
    char keys[4][4] = {
      {'1', '2', '3', 'A'},
      {'4', '5', '6', 'B'},
      {'7', '8', '9', 'C'},
      {'*', '0', '#', 'D'}
    };
    
    byte rowPins[4] = {22, 21, 19, 18};   // connect to the row pinouts of the keypad
    byte colPins[4] = {17, 16, 4, 0};   // connect to the column pinouts of the keypad
    
    // initialize an instance of class NewKeypad
    Keypad myKeypad = Keypad(makeKeymap(keys), rowPins, colPins, 4, 4);
    
    Servo  myservo;     // Create servo object to control a servo
    int servoPin = 15;  // Define the servo pin
    int buzzerPin = 2; // Define the buzzer pin
    
    char passWord[] = {"1234"}; // Save the correct password
    
    void setup() {
      myservo.setPeriodHertz(50);           // standard 50 hz servo
      myservo.attach(servoPin, 500, 2500);  // attaches the servo on servoPin to the servo object
                                            // set the high level time range of the servo motor for an accurate 0 to 180 sweep
      myservo.write(0);                     // Set the starting position of the servo motor
      pinMode(buzzerPin, OUTPUT);
      Serial.begin(115200);
    }
    
    void loop() {
      static char keyIn[4];     // Save the input character
      static byte keyInNum = 0; // Save the the number of input characters
      char keyPressed = myKeypad.getKey();  // Get the character input
      // Handle the input characters
      if (keyPressed) {
        // Make a prompt tone each time press the key
        digitalWrite(buzzerPin, HIGH);
        delay(100);
        digitalWrite(buzzerPin, LOW);
        // Save the input characters
        keyIn[keyInNum++] = keyPressed;
        // Judge the correctness after input
        if (keyInNum == 4) {
          bool isRight = true;            // Save password is correct or not
          for (int i = 0; i < 4; i++) {   // Judge each character of the password is correct or not
            if (keyIn[i] != passWord[i])
              isRight = false;            // Mark wrong passageword if there is any wrong character.
          }
          if (isRight) {                  // If the input password is right
            myservo.write(90);           // Open the switch
            delay(2000);                  // Delay a period of time
            myservo.write(0);            // Close the switch
            Serial.println("passWord right!");
          }
          else {                          // If the input password is wrong
            digitalWrite(buzzerPin, HIGH);// Make a wrong password prompt tone
            delay(1000);
            digitalWrite(buzzerPin, LOW);
            Serial.println("passWord error!");
          }
          keyInNum = 0; // Reset the number of the input characters to 0
        }
      }
    }
    //**********************************************************************************


8. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that press the
keypad to input password with 4 characters. If the input is
correct(Correct password :1234), the servo will move to a certain
degree, and then return to the original position. If the input is wrong,
an input error alarm will be generated.
