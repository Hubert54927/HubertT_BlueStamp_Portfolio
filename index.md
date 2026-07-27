# IoT Plant Watering Kit
Replace this text with a brief description (2-3 sentences) of your project. This description should draw reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Hubert T. | Los Altos High | Mechanical Engineering | Incoming Freshman

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone
Video Link:
<iframe width="560" height="315" src="https://www.youtube.com/embed/uwJGZTC2Gq8?si=ZkvLviiLTtcNf5m3" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

For my final milestone, I installed the blynk app, allowing me to control the motor with a button. I also added automation, which wasn't apart of the orginal project but it felt necessary and more convenient. With the additon of automation, the motor can now automatically turn on or turn off depending on how wet the moisture sensor is. The biggest challenge of this project was having to experiance with most of the parts in this project including the relay, moisture sensor, and teh blynk app. Over the course of building this project I learned alot about arduinos and how to connect them to breadboards, motors, and many more parts need in this project. I also learned about analog and digital pins, and how to code with them. I hope in the future after everthing ive learned at BSE, I can use the knowledge I gained to particpate in more projects that incude mechanical engineering and hopefully even pursue a career in mechanical engineering.


# Second Milestone
Video Link:
<iframe width="560" height="315" src="https://www.youtube.com/embed/mpjEHHbHMYo?si=S6Tgc99Cg-XGqbNA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

For my second milestone, I connected the relay module which allowed the arduino to use its leds to create a sad, nuetral, and happy face depending on how moist the moisture senor is. I made the relay work by connecting it to the breadboard pins that are next to my moisture sensor and arduino digital pin. sad means not enough water in the soil, nuetral means there is a moderate amount of water in the soil, and happy face means there is good amount of water in soil. One thing I found suprising about the project so far is how a breadboard works, by connecting the pins in a horizontal line. Previous challenges that I overcame was learning how to wire the relay module, and connecting it to the moisture sensor and arduino. A couple things I need to do before my final milestone are connecting the motor, setting up the blynk app, and have a full working Iot plant watering system.

# First Milestone
Video Link:
<iframe width="560" height="315" src="https://www.youtube.com/embed/51JzF2bINO4?si=ed-9R_vBSvfdsf9d" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

For my first milestone, I got the moisture soil sensor working. By dipping the moisture sensor in water, I can see on the serial moniter how the sensor reacts ouside of the water compared to inside the water. I learned how to get the moisture sensor working by connecting it to a breadboard and analog pin. This allowed my moisture sensor to become connected to an analog, gnd, and power which makes the whole thing work. Some of the challenges ive faced to finish my first milestone were learning how to wire, use the pins on the arduino, and even some coding. My future challenges for this project are to learn how to code more, and be able to know how to wire proficantly. For my next milestone, I plan to finish connecting my relay to my arduino and moisture sensor so it can display a sad, nuetral, and happy face depending on how wet the moisture senor is.



# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

``` c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:
/*************************************************************
  Blynk is a platform with iOS and Android apps to control
  ESP32, Arduino, Raspberry Pi and the likes over the Internet.
  You can easily build mobile and web interfaces for any
  projects by simply dragging and dropping widgets.

    Downloads, docs, tutorials: https://www.blynk.io
    Sketch generator:           https://examples.blynk.cc
    Blynk community:            https://community.blynk.cc
    Follow us:                  https://www.fb.com/blynkapp
                                https://twitter.com/blynk_app

  Blynk library is licensed under MIT license
  This example code is in public domain.

 *************************************************************
  This example shows how to use Arduino WiFi shield
  to connect your project to Blynk.

  Please update your shield firmware:
    https://www.arduino.cc/en/Hacking/WiFiShieldFirmwareUpgrading

  Feel free to apply it to any other example. It's simple!
 *************************************************************/

/* Comment this out to disable prints and save space */
//#define BLYNK_PRINT Serial

/* Fill in information from Blynk Device Info here */
#define BLYNK_TEMPLATE_ID "TMPL2nQ-97Nif"
#define BLYNK_TEMPLATE_NAME "REMOTE WATERING SYSTEM"
#define BLYNK_AUTH_TOKEN "DBQbDFdSGm09dGzDfsCql6pf2RLqQbbu"

#include <SPI.h>
#include <WiFiS3.h>
#include <BlynkSimpleWifi.h>
#include "Arduino_LED_Matrix.h"
#include <EEPROM.h>

#define moisture_sensor A1
#define relay 7
#define motorPin 8
BlynkTimer timer;
ArduinoLEDMatrix matrix;  //Create an led matrix object

// Your WiFi credentials.
// Set password to "" for open networks.
char ssid[] = "J11";
char pass[] = "Blue@J11";

int eeprom_addr = 0;  //eeprom address
int sensorValue = 0;  // variable to store the value coming from the sensor
int prev_pump_status = 0;
int pump_status = 0;
float moist_percent = 0.00;

const uint32_t HAPPY_LED[] = {
    0x3fc48a95,
    0x58019fd9,
    0x5889871
};

const uint32_t NORMAL_LED[] = {
    0x3fc40298,
    0xd98d8019,
    0x5889871
};

const uint32_t SAD_LED[] = {
    0x3fc48a9d,
    0xd8898018,
    0x71889905
};


BLYNK_WRITE(V1) {     //read data from Blynk cloud
  pump_status = param.asInt();
  EEPROM.write(eeprom_addr,pump_status);
  prev_pump_status = EEPROM.read(eeprom_addr);
  Serial.println(prev_pump_status);
  Serial.println(pump_status);
}

void sendSensor() {   //send data to Blynk cloud
  Blynk.virtualWrite(V0,moist_percent);
}

void init_renesas_MCU_IO() {
  pinMode(relay, OUTPUT);
  pinMode(moisture_sensor, INPUT);
  analogReadResolution(12); //change to 12-bit resolution
  matrix.begin(); //initialise the led matrix*/
}

void track_soil_moisture() {
   //read the value from the sensor:
   sensorValue = analogRead(moisture_sensor);
   moist_percent = 100 - ((float)sensorValue / 4096.0) * 100;
   //moist_percent*=10;
   Serial.println(moist_percent);
   
  if(moist_percent >= 0 && moist_percent < 45){
    Serial.println("DRY");
    matrix.loadFrame(SAD_LED);
    Serial.println(moist_percent);
    digitalWrite(relay, HIGH);
  }
  else if(moist_percent >= 45 && moist_percent <70){
    Serial.println("MODERATE");
    matrix.loadFrame(NORMAL_LED);
    Serial.println(moist_percent);
  }
  else if(moist_percent >= 70){
    Serial.println("WET");
    matrix.loadFrame(HAPPY_LED);
    Serial.println(moist_percent);
    digitalWrite(relay, LOW);
  }
}

void setup() {
  Serial.begin(115200);
  // Debug console
  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);

  init_renesas_MCU_IO();
 
  timer.setInterval(1000L,sendSensor);
  pinMode(motorPin, OUTPUT);

  prev_pump_status = EEPROM.read(eeprom_addr);
  pump_status = prev_pump_status;
}

void loop() {
  Blynk.run();
  timer.run();
  digitalWrite(motorPin, HIGH);
  track_soil_moisture();
  if(pump_status == 0){
    Serial.println("Water pump is off");
    digitalWrite(relay, LOW);
  }
  else if(pump_status == 1){
    Serial.println("Water pump is on");
    digitalWrite(relay, HIGH);
    
  }
  Serial.println("clockwise");
  delay(2000);
  digitalWrite(motorPin, HIGH);
}

```
 


# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino Uno R4 Wifi | Used to automate devices and use code | $27.50 | Link Here|
| DC Water Pump | Used to automate devices and use code | $27.50 | Link here|
| Water Motor | Used to pump and transfer water | $9 | Link Here|
| Moister Sensor 2.0| Used to calculate how moist your plant is | $12 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.amazon.com/AITRIP-Capacitive-Corrosion-Resistant-Electronic/dp/B094J8XD83/ref=sr_1_2?crid=3G8OOYX0G3ZJE&dib=eyJ2IjoiMSJ9.gNHrUBw0qeWZbN2WvG7CtKpS1n_l8NwiG4-9CQlWWlEdkqDKZTo77faprPrwckQMaGnRadhJ033wcLX5Y35j_Z0oEXk6r-wDKmcKpe3jrwghuYHSCSz5AnWWtymczSZdp9ejATRoUxd1tUOcZqMBuNXWNqafu7Mssocb0SXgM68fsYkq_KZvwn1LyofdPC2WcR73uNutawOkbkG3AVOgZrHBF1abcSiHw6NDbMFzBAM.r9o7e4SKj-y5PIgghRYSveB_4UPw_zkR8RgRuDkClig&dib_tag=se&keywords=arduino%2Bmoisture%2Bsensor%2Bv2.0&qid=1784234109&sprefix=arduino%2Bmoister%2Bsensor%2Bv2.0%2Caps%2C159&sr=8-2&th=1)"> Link </a>|
| relay | Used to control the power | $9.60 | <a href="https://www.amazon.com/AITRIP-Channel-Isolation-Compatible-Raspberry/dp/B096M77HCJ/ref=sr_1_4?crid=2BH4MGN7PBAAJ&dib=eyJ2IjoiMSJ9.9cE9x6SBQvFQO7v2ymEMCIjxus7PC4G4oMvaHAW4VvVfEiVv8Y76wMTAb0kL8Lq6pUDsbyhY1PS0eI9IgotBuvKyiZevA0FNOPcGTAaxb_YDe41wnG2j8ZCtJ8nTzfrdkngQnDcDK3_35En_AJTmpjyA6Jro35qBBsmYVdANczu-tnNlgJ-4m5iRyLbpkfzazzoPFcLh9dvFZ5RqpgQnKiuOOrO6qcMSbmiHQvDLAAk.JX5uZNXdoJLVa7wQhILqrcDwEnl2VJ9J78mxQ4CcntI&dib_tag=se&keywords=arduino+relay&qid=1784235112&sprefix=arduino+relay%2Caps%2C178&sr=8-4"> Link </a>|
| Basic Wires | Used to connect things | $6 | <a href="https://www.amazon.com/California-JOS-Breadboard-Optional-Multicolored/dp/B0BRTJXND9/ref=sr_1_5?crid=I3KXD3C9P4JI&dib=eyJ2IjoiMSJ9.qJE7UjNibAzbwpMmx2tJ0xEjvYMaEgz3Vn2NInhtP879k12oMw6KSWbWhXTLBqheeLask61eA6Oq0qbxAdiy6Un1lA2kaC49CZyqQ2mzBQLH0nIWQxo9dIip4IcnR3LTUiWd-D0ljV5kVq57Xv7e7NRNIzBDcUkztzcf4JJbVLBhw9AqCZS1CUk2oI7GUDolv1p4_Z8VKNYFZc5ixbrC7Ls32uPGH__XqCKjoUSZbek.ifzIYQKazTJcT9L9J2z1C6fYDG43k7TdNV_VMWiij2A&dib_tag=se&keywords=arduino%2Bwires&qid=1784235312&sprefix=arduino%2Bwire%2Caps%2C180&sr=8-5&th=1"> Link </a>|
| Bread Board | Used to connect wires | $6 | <a href="https://www.amazon.com/ELEGOO-tie-points-breadboard-Arduino-Jumper/dp/B01EV640I6/ref=sr_1_15?crid=1VLPDDYOEI0GA&dib=eyJ2IjoiMSJ9.5Z5yTwL-oa1r18Ah_zf9OdziZtM7NtJzJKlf3z7Il1RZRsLHHdDXy8k48WgaDzgsQ6w8v_YzyQq3oeGgxJ3klrEDkcVpEPBYptdRMP2WHOJrLcVPkMI1WLOfSnmWxa_PX-ncmj_znz17XEYYDeVdULS2gqZ3hhaQGZ-6h30Or3n_P_I6L-77nwAcMiJI4FJ-rduK1FPphqLdszT0dOnZyfdPs2IFMC3IP1fo_TcAAg0.Rh4W-dAIGtIMk-LDxF_PuyGpNhbEYpJ_0MmXhVE0lYc&dib_tag=se&keywords=breadboard&qid=1784235446&sprefix=breadboard%2Caps%2C220&sr=8-15"> Link </a>|
| 9v battery | Used to power your arduino | $13 | <a href="https://www.amazon.com/Amazon-Basics-Performance-All-Purpose-Batteries/dp/B00MH4QM1S/ref=sr_1_5?crid=1Q4TLA99SWS95&dib=eyJ2IjoiMSJ9.8xIC2eXJTnIdYA30fCJOn_iE79m41H7SomYYi3eBFPuRrOWWZozBDhkkdClRxooDpdDJtzh1DNj8RgSb0qzsUJZrK8eMdAIMmMzElqGcn9sX00SrTI3KhFDVcNLPxrHqJW5MDlgeVf_ua41n17cyrj_vVKfKxTZFw_OwfbPcUFdX7K19ZfkuDrk5mt7fvALu07EOvXHjpxO-wlxF6f-crW0HqaN64OkzDmoPot2ObqVWe-Vd-aSN-xvkvojVa16jGshR99AncF8Q9DmA0zjDsNu1Yrxhzp7VJZL1LrlbeXeg.srOGvZpM8Bz18V8yE5IxvnobDWkCRTyBad_AphAWPnE&dib_tag=se&keywords=batteries+9v&qid=1784235662&rdc=1&sprefix=batteries+9%2Caps%2C186&sr=8-5"> Link </a>|




# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)


