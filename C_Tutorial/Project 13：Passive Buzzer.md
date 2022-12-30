# Project 13：Passive Buzzer

1. Introduction:

In a previous project, we studied an active buzzer, which can only make
a sound and may make you feel very monotonous. In this project, we will
learn a passive buzzer and use the ESP32 control it to work. Unlike the
active buzzer, the passive buzzer can emit sounds of different
frequencies.

2. Components：

<table>
<tbody>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/b8f46441af8a96464075d155e6ff7610.jpeg" style="width:1.29375in;height:0.63125in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/e380dd26e4825be9a768973802a55fe6.png" style="width:0.59306in;height:1.45486in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/d1ea1bb2b2749820cab389d5b85b838b.png" style="width:0.52708in;height:0.63333in" /></td>
<td></td>
</tr>
<tr class="even">
<td>ESP32*1</td>
<td>Breadboard*1</td>
<td>Passive Buzzer *1</td>
<td></td>
</tr>
<tr class="odd">
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/9197d4aff9356c585b7ef68e33a6881d.png" style="width:0.27986in;height:1.08819in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/098a2730d0b0a2a4b2079e0fc87fd38b.png" style="width:0.90833in;height:0.23681in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/fa38b2e3964d342d0a5c446490ff4811.png" style="width:0.59236in;height:0.57014in" /></td>
<td><img src="https://raw.githubusercontent.com/keyestudio/KS5010-KS5010F-Keyestudio-ESP32-Learning-Kit-Ultimate-Edition-Arduino/master/media/7dcbd02995be3c142b2f97df7f7c03ce.png" style="width:1.05903in;height:0.56667in" /></td>
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

![](/media/8d0020e53824072cbe9d4f7d2f8acb4f.png)

**Passive buzzer:** A passive buzzer is an integrated electronic buzzer
with no internal vibration source and it has to be driven by 2K-5K
square waves, not DC signals. The two buzzers are very similar in
appearance, but one buzzer with a green circuit board is a passive
buzzer and the other buzzer with black tape is an active buzzer. Passive
buzzers cannot distinguish between positive polarity while active
buzzers can.

![](/media/fc42c5ed014609ff0b290ee5361bb2fd.png)

**Transistor:** Please refer to Project 12.

4. Wiring diagram:

![](/media/9c12d89ce3f10c838e63f1334f41fc9e.png)

5. Project code：

You can open the code we provide:

The code used in this project is saved in folder **“2. Windows
System\\2. C\_Tutorial\\2. Projects\\Project 13：Passive
Buzzer\\Project\_13\_Passive\_Buzzer****”**.

    //**********************************************************************
    /*
     * Filename    : Passive Buzzer
     * Description : Passive Buzzer sounds the alarm.
     * Auther      : http//www.keyestudio.com
    */
    #define LEDC_CHANNEL_0 0
    
    // LEDC timer uses 13 bit accuracy
    
    #define LEDC_TIMER_13_BIT  13
    
    // Define tool I/O ports
    
    #define BUZZER_PIN  15
    
    //Create a musical melody list, Super Mario
    
    int melody[] = {330, 330, 330, 262, 330, 392, 196, 262, 196, 165, 220, 247, 233, 220, 196, 330, 392, 440, 349, 392, 330, 262, 294, 247, 262, 196, 165, 220, 247, 233, 220, 196, 330, 392,440, 349, 392, 330, 262, 294, 247, 392, 370, 330, 311, 330, 208, 220, 262, 220, 262,
    
    294, 392, 370, 330, 311, 330, 523, 523, 523, 392, 370, 330, 311, 330, 208, 220, 262,220, 262, 294, 311, 294, 262, 262, 262, 262, 262, 294, 330, 262, 220, 196, 262, 262,262, 262, 294, 330, 262, 262, 262, 262, 294, 330, 262, 220, 196};
    
    //Create a list of tone durations
    
    int noteDurations[] = {8,4,4,8,4,2,2,3,3,3,4,4,8,4,8,8,8,4,8,4,3,8,8,3,3,3,3,4,4,8,4,8,8,8,4,8,4,3,8,8,2,8,8,8,4,4,8,8,4,8,8,3,8,8,8,4,4,4,8,2,8,8,8,4,4,8,8,4,8,8,3,3,3,1,8,4,4,8,4,8,4,8,2,8,4,4,8,4,1,8,4,4,8,4,8,4,8,2};
    void setup() {
    pinMode(BUZZER_PIN, OUTPUT); // Set the buzzer to output mode
    }
    
    void loop() {
    
      int noteDuration; //Create a variable of noteDuration
    
      for (int i = 0; i < sizeof(noteDurations); ++i)
    
      {
          noteDuration = 800/noteDurations[i];
    
          ledcSetup(LEDC_CHANNEL_0, melody[i]*2, LEDC_TIMER_13_BIT);
    
          ledcAttachPin(BUZZER_PIN, LEDC_CHANNEL_0);
    
          ledcWrite(LEDC_CHANNEL_0, 50);
    
          delay(noteDuration * 1.30); //delay
      }
    }
    //**********************************************************************

6. Project result：

Compile and upload the code to ESP32, after the code is uploaded
successfully, power up with a USB cable and you will see that the
passive buzzer plays music.
