# IoT Plant Watering Kit
Replace this text with a brief description (2-3 sentences) of your project. This description should draw reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Hubert T. | Los Altos High | Mechanical Engineering | Incoming Freshman

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
For my final milestone, I installed the blynk app, allowing me to control the motor with a button. I also added automation, which wasn't apart of the orginal project but it felt necessary and more convenient. With the additon of automation, the motor can now automatically turn on or turn off depending on how wet the moisture sensor is. The biggest challenge of this project was having to experiance with most of the parts in this project including the relay, moisture sensor, and teh blynk app. Over the course of building this project I learned alot about arduinos and how to connect them to breadboards, motors, and many more parts need in this project. I also learned about analog and digital pins, and how to code with them. I hope in the future after everthing ive learned at BSE, I can use the knowledge I gained to particpate in more projects that incude mechanical engineering and hopefully even pursue a career in mechanical engineering.
For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
For my second milestone, I connected the relay module which allowed the arduino to use its leds to create a sad, nuetral, and happy face depending on how moist the moisture senor is. I made the relay work by connecting it to the breadboard pins that are next to my moisture sensor and arduino digital pin. sad means not enough water in the soil, nuetral means there is a moderate amount of water in the soil, and happy face means there is good amount of water in soil. One thing I found suprising about the project so far is how a breadboard works, by connecting the pins in a horizontal line. Previous challenges that I overcame was learning how to wire the relay module, and connecting it to the moisture sensor and arduino. A couple things I need to do before my final milestone are connecting the motor, setting up the blynk app, and have a full working Iot plant watering system.

# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For my first milestone, I got the moisture soil sensor working. By dipping the moisture sensor in water, I can see on the serial moniter how the sensor reacts ouside of the water compared to inside the water. I learned how to get the moisture sensor working by connecting it to a breadboard and analog pin. This allowed my moisture sensor to become connected to an analog, gnd, and power which makes the whole thing work. Some of the challenges ive faced to finish my first milestone were learning how to wire, use the pins on the arduino, and even some coding. My future challenges for this project are to learn how to code more, and be able to know how to wire proficantly. For my next milestone, I plan to finish connecting my relay to my arduino and moisture sensor so it can display a sad, nuetral, and happy face depending on how wet the moisture senor is.

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
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

 


# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino Uno R4 Wifi | Used to automate devices and use code | $27.50 | <[a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-](https://www.amazon.com/Arduino-UNO-WiFi-ABX00087-Bluetooth/dp/B0C8V88Z9D/ref=sr_1_3?crid=26TAKYROGWLH8&dib=eyJ2IjoiMSJ9.hgTVTNipNCjb6SRiDR3Picrx_Z8KEkfOHx4nsM_zlVhFFqjUlNq3p9FBo_zaOP_R5jfvfm3HdEZqLFYoS6JIZK3HELYf5gmdzPpxCbW80mwyEBLXStP__wBMgmgZ9KMiPtSyq5OcZm4CDi2Wd-iDf8tlvuMHk6x-y0D2sQ6dj0aWjBRn5AGDO_8eyxbEBQ7DhR7OhtiXvfIYMq1rNufmj_SNzw5SRYep15DLRpDsBUk._Kgd2w0uLwM7paSheRkUT9vcIXVRSAlRkUsh_OILmiQ&dib_tag=se&keywords=ARDUINO+R4+UNO&qid=1784155190&sprefix=arduino+r4+uno%2Caps%2C178&sr=8-3)R3/dp/B008GRTSV6/"> Link </a> |
| Water Motor | Used to pump and transfer water | $9 | <amazon.com/ALAMSCN-Submersible-Aquariums-Fountain-Hydroponics/dp/B08PBQ1N1G/ref=sr_1_5?crid=2JWOQU9ZTCO66&dib=eyJ2IjoiMSJ9.PmsVVF38wHQKauTJygc25JyPu7crquC4YOZlIMymjJPTMnIuGBcVTIldOe8Yqu6_IxwuKyPK9PJ2wl5FfiXSEG-WITib7oOHwgcEOkWyz96z-P521Odh4qBJdFunlMt2yJ3qSBoKtveqhV10jCrankhwfkZe-QqnL9j-_ro4xqm_LRoiAv6RopaIJgJH73K7STwZx7ed9hc9hHL-eS3XpQmsjA_qGuQrjXnTngsg1dNjkREqZ7E9z3gOa5JXMixtSXpEQFDLbBe7GUEK3gNak20Lla0cwukXiXQ9ykhSSJw.VokMlnaZpl5zu8g8rcrNjNV1kmZ79L-6oBjH52hUty0&dib_tag=se&keywords=dc+water+pump+arduino&qid=1784156502&sprefix=dc+water+pump+arduino%2Caps%2C253&sr=8-5"> Link </a> |
| Moister Sensor @2.0| What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
