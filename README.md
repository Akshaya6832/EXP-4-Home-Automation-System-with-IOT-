# EXP-4-Home-Automation-System-with-IOT

# Aim:
To make a Lamp at home (230 V AC) On / Off using ESP8266, IFTT Google Assistance and Blynk IoT mobile application. 

# Hardware / Software Tools required :
- PC with Internet connection
- Micro USB cable
- Wifi connection for ESP8266 (Use any mobile hotspot or Router)
- ESP8266 Board
- Mobile Phone with Blynk App installed
- IFTT for Google Voice Assistance
- 9 W Bulb and Relay control
- Arduino software 
- Jumper Wires

# Circuit Diagram:

<img width="1919" height="1139" alt="image" src="https://github.com/user-attachments/assets/3b26467f-1da3-409e-8db2-6829cbe07b01" />

# Theory: 

Blynk is an IoT platform for iOS or Android smartphones that is used to control Arduino, Raspberry Pi and NodeMCU via the Internet. This application is used to create a graphical interface or human machine interface (HMI) by compiling and providing the appropriate address on the available widgets.In this experiment we use ESP8266 to control a 220-volt lamp from a web server. But you can also use the same procedure to control fans, lights, AC, or other electrical devices that you want to control remotely.
Relay is an electromechanical device that is used as a switch between high current and low current devices. When the coil in the relay gets fully energized, the contact shifts from the normally open position to the normally closed position. Light bulbs usually operate on 120V or 220V AC power supply. We cannot interface these AC loads directly with the ESP8266 development board, or it will damage the board. We have to use a relay between the ESP8266 and the lamp. 
Google Assistant and IFTTT work together to let you control services with voice commands. When you say a set phrase, Google Assistant processes it and sends it to IFTTT as a trigger. If the phrase matches an applet you've created, IFTTT performs the linked action—like turning on a light or sending a message. Everything runs in the cloud, making it easy to automate tasks with just your voice, as long as the command is correctly matched and all services are online.
When we apply an active high signal to the signal pin of the relay module from any microcontroller like ESP8266, the relay contact moves from the normally open to the normally closed position. It makes the circuit complete, and the output load turns on.


# Program:
```c
#include <LiquidCrystal.h>
#include<Servo.h>
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
const int trig_pin=10;
const int echo_pin=7;
long duration;
int distance;
int servopin=8;
Servo servo_test;
const int pirpin=13;
const int light=6;
int sensorstate=0;
const int temp_pin=A0;
float temp;
const int motor=9;

void setup()
{
  pinMode(temp_pin,INPUT);
  pinMode(trig_pin,OUTPUT);
  pinMode(echo_pin,INPUT);
  Serial.begin(9600);
  servo_test.attach(servopin);
  pinMode(light,OUTPUT);
  pinMode(pirpin,INPUT);
  lcd.begin(16, 2);
  lcd.setCursor(3, 0);
  lcd.print("G  CHANDAN");
  lcd.setCursor(4, 1);
  lcd.print("PROJECTS");
  delay(800);
  lcd.clear();
  lcd.setCursor(4, 0);
  lcd.print("PROJECT");
  lcd.setCursor(0, 1);
  lcd.print("HOME AUTOMATION");
  delay(800);
  lcd.clear(); 
}

void loop()
{
  digitalWrite(trig_pin,LOW);
  delayMicroseconds(2);
  digitalWrite(trig_pin,HIGH);
  delayMicroseconds(10);
  digitalWrite(trig_pin,LOW);
  duration = pulseIn(echo_pin,HIGH);
  distance= duration*0.034/2;
  
  if(distance<100)
  {
  servo_test.write(90);
  delay(3000);
  servo_test.write(0);
  delay(5000);
  lcd.setCursor(0,1);
  lcd.print("   open the gate  ");
  }
  else
  {
      
   lcd.setCursor(0,1);
   lcd.print("  close the gate  ");
  }
    
   sensorstate=digitalRead(pirpin);
  if(sensorstate)
  {
    digitalWrite(light,HIGH);
    lcd.setCursor(0,1);
    lcd.print("  On the lights   ");
    delay(1000);
  }
  else
  {
    digitalWrite(light,LOW);
     delay(1000);
  }
  
  temp=analogRead(temp_pin)*0.00488*100;
  Serial.print("Temperature: ");
  Serial.println(temp,0);
  delay(2000);
  if(temp>=60)
  {
    lcd.clear();
    digitalWrite(motor,1);
    lcd.setCursor(0,1);
    lcd.print("FAN IS ON");
    delay(1000);
   }
  else
 {
    lcd.clear();
    lcd.setCursor(0,1);
    lcd.print("FAN IS OFF");
    digitalWrite(motor,0);
}
}
  
```


# Procedure:
---
•	Sure! Here’s your provided content formatted neatly for a **GitHub README.md** file (no extra additions):

---

## Procedure:

* Make the circuit connection as per the diagram. In the mobile, download and “Blynq IoT” application using Google Play Store and install it. Create login ID and Password.
* Connect the **IN pin** of the Relay module to **D1 pin** of NodeMCU (ESP8266).
* Connect **VCC** of the Relay to **VCC** of NodeMCU. Connect **GND** of the Relay to **GND** of NodeMCU.
* Connect your **AC bulb** to the Relay’s switch terminal securely.
* Install **ESP8266 board** in Arduino IDE via Board Manager. Select board: **NodeMCU 1.0 (ESP-12E Module)**.
* Include necessary libraries: **ESP8266WiFi** and **ESP8266WebServer**.
* In the code, configure **Wi-Fi SSID** and **Password**.
* Set up a **web server** that responds to `/on` and `/off` URLs.
* Upload the code to the ESP8266 using a **micro USB cable**.
* **Get Local IP Address:** After uploading, open Serial Monitor to find the local IP address of ESP8266.
* **Create Applets on IFTTT:** For "This", select Google Assistant → "Say a simple phrase". Command: *"Turn on the light"*. For "That", choose Webhooks → "Make a web request".
* Repeat to create another applet for the "Turn off the light" command with the respective URL.
* **Test the System:** Google Assistant triggers IFTTT → sends Webhook to ESP8266 → turns ON the relay (light).
* Say *"Turn off the light"* to switch it **OFF**, say *"Turn on the light"* to switch it **ON**.


---
# Output:

https://github.com/user-attachments/assets/6dc64c44-a1a7-4f52-a1b1-d8108ced1dcc

<img width="1913" height="1144" alt="image" src="https://github.com/user-attachments/assets/576fba84-51ec-48a2-8be2-f052f7a4bf5e" />

---
# Result:

Thus, Home Automation System with IOT was successfully implemented using TinkerCad.
