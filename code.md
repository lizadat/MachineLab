# CODE 

Current issue with this code is that the colors of the cloud are not changing, meaning that fadeAll method is not working. 

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
const long interval_color = 1000;


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
    Serial.println("fadeALL - 1");
    fadeAll(65, 0, 168, 128, 244, 255, 100);
    Serial.println("fadeAll - 2");
    fadeAll(128, 244, 255, 23, 7, 245, 100);
    Serial.println("fadeAll - 3");
   } 
}

void fadeAll(int r1, int g1, int b1, int r2, int g2, int b2, int steps) {
  unsigned long currentMillisCol = millis();

   //if (currentMillisCol - previousMillisColor >= interval_color){
    //previousMillisColor = currentMillisCol;
    for (int i = 1; i < steps; i++) {
      if (currentMillisCol - previousMillisColor >= interval_color){
      previousMillisColor = currentMillisCol;
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
}
```
</details>

This is the initial code for fadeAll. I tried to incorporate the millis method for that, but it is not working. 

<details>
<summary>Click to toggle contents of code</summary>

```
void loop() {
  //r1, g1, b1, r2, g2 ,b2 , fade rate , steps

  fadeAll(23, 7, 245, 65, 0, 168, 50, 100);
  fadeAll(65, 0, 168, 128, 244, 255, 50, 100);
  fadeAll(128, 244, 255, 23, 7, 245, 50, 100);
}

void fadeAll(int r1, int g1, int b1, int r2, int g2, int b2, int fadeRate, int steps) {
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
    delay(fadeRate);
  }
```
</details>
