# Progress

## In class
The lecture in class was very helpful for understanding of how everything will look like in the end. Even though we are still in the process of developing our project, but it is good to have in mind what is coming next so we can cover some steps now (for instance making the wires longer so that they would reach Arduino and powering station on the back of the platform). 
We continued making progress on our SkyRide during the class.
First of all the 3D prints (two wheels) were completed so we replaced our old ones with the new. Since we had enough space on the wheels inside to attach the holders we drilled the filles for that. There was one mistake made though as we drilled one big hole for the shaft and we did not used it because the shaft is not supposed to go to the wheel. It is a good reminder for the future: Score (think) twice before you cut (drill) once. It does not harm our project except how it will look like in the end. 
Here are the photos from how we attached the wheels. 

<img src="https://github.com/lizadat/MachineLab/assets/98390904/a5f8392f-ab30-42f3-99d8-d76955cdf2a0" width="30%" height="30%">   <img src="https://github.com/lizadat/MachineLab/assets/98390904/dc493a9e-7485-4e84-bdfd-d1cba8a523cf" width="30%" height="30%">   
<img src="https://github.com/lizadat/MachineLab/assets/98390904/8a36f51b-ff61-4201-9923-4839c22eb706" width="30%" height="30%">   <img src="https://github.com/lizadat/MachineLab/assets/98390904/d0b58e33-6be9-437a-bc22-f059c1e0070b" width="30%" height="30%">


After we attached the new wheels we wanted to try out how everything worked. Howeve we realized that our motor has only one wire attached to it AND there is no access to the place where the wires are attached. As a result we had to unscrew our aluminium shaft holder and solder the wires to the motor. Then we attached it back to where it was supposed to be. 
We then connected the motor for the ride and servo for the clouds and made all the mechanisms moving! It actually works! 
Only thing we need to do is to make a rope for ride a bit longer, but we will see how the cars will impact it. 
And, speaking about the cars, we laser cut one, but the thickness of the material is very small, so we did uuse the glue to put it all together. The car turned out very light, which is both good and bad: good - it does not put any pressure on the rope; bad - it is floating and is the weight is not equally distributed. We want to get the ply wood and laser cut again and see how it will turn out. We will also need to think of how to attach it to the rope. 

We wanted to continue with wiring everything so we connected one cloud to the Arduino as well and that's where the problem arose. The code goes in a loop and starts with one thing (turning the motor) and continues after that with another one (lighning the cloud). We need to use the millis concept for the code in order to make everything run simultaneously.

Nevertherless, this is our current progress in a video after the class work:
https://github.com/lizadat/MachineLab/assets/98390904/b164e8d1-fad5-4e15-83b9-f0bcc54e05df


## Homework

For working on our project we got together and built a second ride. Initially we were planning on doing two rides, one of which would be diagonal, but we decided to not overcomplicate our project and focus more on other small, but more important details (decoration, final looks). 
This week we built a secodn ride. We asked the professor to cut the shafts for us the right height - the secodn ride is half size the first one. We did all the measurements of where the second ride will be located, drilled the holes for it. We also made an aluminium bracket to fix the motor to the bottom. The wheels were already printed, so we also drilled the holes in there and attached the corresponding pieces. 

<img src="https://github.com/lizadat/MachineLab/assets/98390904/2779b333-aef0-408b-a1b1-921d1696d028" width="50%" height="50%">


As we have already gone through the process of putting the ride together, putting the second ride was much easier. We also soldered the wires right away, because last time we had to unscrew some stuff. Also we cut a new rope, making it a bit longer, so that it does not bend that much the first ride.
NOTE: from now one the first ride will be called 'the back ride', and the second - the new we made today - 'the front ride'.

In order to test everything we connected both motors to power ad ground and it all worked. We also decided on doing a support for the front ride as well, so that it is stronger and does not bend because of the rope. 
This is how everything looked like in the front in the end. 

https://github.com/lizadat/MachineLab/assets/98390904/b2ebfb70-786f-4565-b90a-908bcd8b6a1d

As the assignment for this week was to do the wiring (organize it in some ways).

The clouds have quite a complicated system of wiring because there are 8 of them. After adding the right length wires we realized that it is most probably just wasting the resources. We came to the conclusion that all the power and ground wires have to be connected somewhere where they all are getting together (where the frame is attached to the motor) and the wires which are supposed to go to Arduino will be long. 


<img src="https://github.com/lizadat/MachineLab/assets/98390904/3749e278-001f-4823-80cf-d932aab7cdb0" width="50%" height="50%">


We attached the Arduino to metal holder (with the help of YouTube tutorial, cause we could not figure out how to connect them, lol) provided by the professor. We also attached the holder itself to the back with the velcro. Also we have a breadboard sticked on the back temporarily. 

As we at this point had two motors, so we decided to use the zippers to hold the motor wires together and also put the tags saying what those wires go to. 

<img src="https://github.com/lizadat/MachineLab/assets/98390904/bedc55f7-ce0e-4715-9ffa-17e6b240e7ce" width="50%" height="50%">


CHALLENGE: 
Th ebiggest challenge this week was the coding part. As we decided that the best way for all the things to work together would be using the millis method, we had to change the code. However, it still does not work. The clouds can change and the motor can move separetely well, but not when together. We would probablu have to seek the help from the professor. 
This is the code we have as of now:

<details>
<summary>Click to toggle contents of code</summary>

```
#include <Servo.h>
#include <Adafruit_NeoPixel.h>
#define PIN 5
#define NUMPIXELS 20
Adafruit_NeoPixel pixels = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

Servo myservo; 

int pos = 95;  

int beginPos = 95;   // initial position of the servo
int targetPos = 115;   // target position of the servo
int step = 1;  // step size for each movement
unsigned long previousMillisMotor = 0;  // variable to store the last time the servo was moved
unsigned long previousMillisNeopixel = 0;  // variable to store the last time the servo was moved
unsigned long previousMillisColor = 0;  // variable to store the last time the servo was moved
const long interval_motor = 100;  // interval at which to move the servo (in milliseconds)
const long interval_neopixel = 1000;
const long interval_color = 50;


void setup() {
  // set the digital pin as output:
  myservo.attach(9); 
  myservo.write(pos);
  pixels.begin();
  pixels.show();
  Serial.begin(9600);
}

void loop() {
  motor_check();
  neopixel();
}

void motor_check(){
  unsigned long currentMillisMotor = millis();  // get the current time

  // check if it's time to move the servo
  if (currentMillisMotor - previousMillisMotor >= interval_motor) {
    previousMillisMotor = currentMillisMotor;

    // move the servo towards the target position
    pos += step;
    if (pos >= targetPos || pos <= 95) {
      step *= -1; // Reverse direction when reaching target position or start position
    }
    myservo.write(pos);  // move the servo to the new position
  }
}

void neopixel(){
  unsigned long currentMillisNeo = millis();

  if (currentMillisNeo - previousMillisNeopixel >= interval_neopixel){
    previousMillisNeopixel = currentMillisNeo;
    fadeAll(23, 7, 245, 65, 0, 168, 100);
    fadeAll(65, 0, 168, 128, 244, 255, 100);
    fadeAll(128, 244, 255, 23, 7, 245, 100);
  } 
}

void fadeAll(int r1, int g1, int b1, int r2, int g2, int b2, int steps) {
  unsigned long currentMillisCol = millis();

   if (currentMillisCol - previousMillisColor >= interval_color){
    previousMillisColor = currentMillisCol;
    for (int i = 1; i < steps; i++)
    {
      uint8_t red = (((r1 * (steps - i)) + (r2 * i)) / steps);
      uint8_t green = (((g1 * (steps - i)) + (g2 * i)) / steps);
      uint8_t blue = (((b1 * (steps - i)) + (b2 * i)) / steps);
      // Sets the pixels to the color adjusted in the fade
      for (int i = 0; i < NUMPIXELS; i++) {
        pixels.setPixelColor(i, red, green, blue);
      }
      pixels.show();
    }
   }
}
```
</details>

Plans for future:
- As soon as ply wood arrives - laser cut the cars
- 3D print the parts of the cars which will attach the cars to the rope
- Make an aluminuim holder for the front motor
- Debug the code
- Wire up all the clouds
