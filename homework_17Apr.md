# Progress
Presentation: Kinetoscope. [Link](https://www.canva.com/design/DAGBopYjjKA/2alR02OHYtEwDWe5YRsPSA/edit?utm_content=DAGBopYjjKA&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

### In class
Since we had some time during our class on Monday, we continued working on our front ride. We added the aluminium holder to hold the shaft and prevent it from leaning to the sides. We had to think a lot on how to attach it as precise as possible because its bending was not precise. But we managed to do it and here is a final look:

<img src="https://github.com/lizadat/MachineLab/assets/98390904/6762129a-1a6f-4401-9847-fa3493d217cb" width="50%" height="50%">


During the class on Wednesday we continued soldering the wires so that they are longer and can reach Arduino on the back. During the class we finished 4 clouds and connected the to the frame in a corresponding position. Moreover, we put the tags on each so that later on during wiring everything and coding each clouds separetely we will be able to figure out which cloud is where. 

<img src="https://github.com/lizadat/MachineLab/assets/98390904/6b3315fa-10e2-4316-a014-2c2230c119be" width="50%" height="50%">


### Homework
After the classtime we finished all the clouds and attached them. We might change the heigh of each cloud later on, but currently it looks pretty well. Soldering and making all the clouds in general was quite a repetitive and not fun task to do, but it helped to practice my soldering skills. 
Before we had the 

Professor has helped to figure out the code for the cloud to fade. Previously we had an issue with delay, so we used the millis method as the result. 
I combined the code for the neopixel fading the the servo motor. 


<details>
<summary>Click to toggle contents of code for the motor with new degree values</summary>

```
//
// fadeNeoWithouDelay
//
// This program fades the three colors of NeoPixel without using delay
// By default, each color goes from 0 to 255 in increments of 1
// but the red values can be changed with setRedValues(). Of course 
// similar functions for green and blue can also be written. This is 
// left as an exercise to the reader.

// 03 Apr 2024 - MS - Initial entry

#include <Servo.h>
#include <Adafruit_NeoPixel.h>

// SERVO PIN NUM 9!!!!
Servo myservo;

int pos = 95;  

int beginPos = 95;   // initial position of the servo
int targetPos = 115;   // target position of the servo
int step = 1;  // step size for each movement
unsigned long previousMillisMotor = 0;
const long interval_motor = 100;

class NeoPixelFader
{
    int neoPixelPin;
    int numberOfPixels;
    int delayBetweenSteps; // this could be per each color too

    // these are initial values that can be
    // changed with setRedRange etc.
    //
    // really this should be in a sub-class
    // because they all do the same thing
    // just with different variables
    uint8_t redMinValue = 0;
    uint8_t redMaxValue = 255;
    uint8_t redCurrentValue = 0;
    uint8_t redIncrementAmount = 1;
    unsigned long redPreviousMillis = 0;

    uint8_t greenMinValue = 0;
    uint8_t greenMaxValue = 255;
    uint8_t greenCurrentValue = 0;
    uint8_t greenIncrementAmount = 1;
    unsigned long greenPreviousMillis = 0;

    uint8_t blueMinValue = 0;
    uint8_t blueMaxValue = 255;
    uint8_t blueCurrentValue = 0;
    uint8_t blueIncrementAmount = 1;
    unsigned long bluePreviousMillis = 0;

    Adafruit_NeoPixel pixels;

    // Constructor
  public:
    NeoPixelFader(int _neoPixelPin, int _numberOfPixels,
                  int _delayBetweenSteps)
    {
      neoPixelPin = _neoPixelPin;
      numberOfPixels = _numberOfPixels;
      delayBetweenSteps = _delayBetweenSteps;
      // currently every color gets the same delay
      // but this could also be configured individually

      pixels = Adafruit_NeoPixel(numberOfPixels, neoPixelPin, NEO_GRB + NEO_KHZ800);
    }

    void begin()
    {
      pixels.begin();
    }

    void setRedValues(
      uint8_t _redMinValue,
      uint8_t _redMaxValue,
      uint8_t _redCurrentValue,
      uint8_t _redIncrementAmount)
    {
      redMinValue = _redMinValue;
      redMaxValue = _redMaxValue;
      redCurrentValue = _redCurrentValue;
      redIncrementAmount = _redIncrementAmount;
    }

    void update()
    {
      updateRed();
      updateGreen();
      updateBlue();
    }

    // for debugging
    void print() {
      Serial.print("Red = ");
      Serial.print(redCurrentValue);
      Serial.print("\tGreen = ");
      Serial.print(greenCurrentValue);
      Serial.print("\tBlue = ");
      Serial.print(blueCurrentValue);
      Serial.println();
    }

    void updateRed() {
      unsigned long currentMillis = millis();
      if (currentMillis - redPreviousMillis >= delayBetweenSteps) {

        // calculate the next value of colors
        redCurrentValue += redIncrementAmount;

        // If we've reached the minimum or maximum, change direction
        if ((redCurrentValue >= redMaxValue) || (redCurrentValue <= redMinValue)) {
          redIncrementAmount = -redIncrementAmount;
        }

        // update the NeoPixels
        for (int i = 0; i < numberOfPixels; i++) {
          pixels.setPixelColor(i, redCurrentValue, greenCurrentValue, blueCurrentValue);
        }
        pixels.show();

        // update previousMillis
        redPreviousMillis = currentMillis;
      }
    }

    void updateGreen() {
      unsigned long currentMillis = millis();
      if (currentMillis - greenPreviousMillis >= delayBetweenSteps) {

        // calculate the next value of colors
        greenCurrentValue += greenIncrementAmount;

        // If we've reached the minimum or maximum, change direction
        if ((greenCurrentValue >= greenMaxValue) || (greenCurrentValue <= greenMinValue)) {
          greenIncrementAmount = -greenIncrementAmount;
        }

        // update the NeoPixels
        for (int i = 0; i < numberOfPixels; i++) {
          pixels.setPixelColor(i, redCurrentValue, greenCurrentValue, blueCurrentValue);
        }
        pixels.show();

        // update previousMillis
        greenPreviousMillis = currentMillis;
      }
    }

    void updateBlue()
    {
      unsigned long currentMillis = millis();
      if (currentMillis - bluePreviousMillis >= delayBetweenSteps) {

        // calculate the next value of colors
        blueCurrentValue += blueIncrementAmount;

        // If we've reached the minimum or maximum, change direction
        if ((blueCurrentValue >= blueMaxValue) || (blueCurrentValue <= blueMinValue)) {
          blueIncrementAmount = -blueIncrementAmount;
        }

        // update the NeoPixels
        for (int i = 0; i < numberOfPixels; i++) {
          pixels.setPixelColor(i, redCurrentValue, greenCurrentValue, blueCurrentValue);
        }
        pixels.show();

        // update previousMillis
        bluePreviousMillis = currentMillis;
      }
    }
};

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


// pin, number of pixels, delay between steps
NeoPixelFader cloud1(A5, 20, 10); 

void setup() {
  Serial.begin(9600);
  myservo.attach(9); 
  myservo.write(pos);
  // parameters are
  // redMinValue, redMaxValue, redCurrentValue,redIncrementAmount)
  cloud1.setRedValues( 50, 100, 100, -1);
  cloud1.begin();
}

void loop() {
  motor_check();
  cloud1.update();
  // cloud1.print();
}
```
</details>


In the end everything worked out well. The motor and neopixel go together. Here is a video of it from two perspectives: side and front. 

https://github.com/lizadat/MachineLab/assets/98390904/0223217a-064d-4cd7-b2d7-1dcaed947f9b


https://github.com/lizadat/MachineLab/assets/98390904/4e4c089b-9ab0-4191-966d-636d5fe0a6d5


Problems we are facing:
We need to laser cut the cars, but the laser cutter in the lab broke. We reached out to the advanced workshop, so maybe they will be able to help us. 

Future steps: 
- We will add more clouds to the code and will connect them to the Arduino and use additional voltage for neopixel
- We will figure out how to laser cut the cars
- We will 3D print the holders for the cars
- We will start working on the design for a bottom of the ride. We want to laser cut the skylines of different cities to fill that space and craete an illusion that the ride is very high. 

