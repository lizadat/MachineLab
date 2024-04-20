# Progress

This week was alittle bit challenging to work on the project due to weather conditions.
On Monday I was able to spray paint the back and bottom of our project and it was just before the storm. Perfect timing! 
I painted the back with blueish and white colors and made it look like the sky, as our project is a SkyRide and the clouds are a big part of the project.
The bottom I decided to do green, which is a natural color for the ground. We plan to add the city on the bottom, but having some kind of color there is good. 
Here is the progress and the result:

<img src="https://github.com/lizadat/MachineLab/assets/98390904/57e439da-d180-409b-9214-73f056d42bd0" width="50%" height="50%">

<img src="https://github.com/lizadat/MachineLab/assets/98390904/1a334f23-910d-4553-b002-b1b0d19325b7" width="50%" height="50%">


Because I have done the decorating (spray paint) part, I could continue working with the wiring. The biggest part was to connect all the clouds. I ended up soldering all power (red) wires together and all ground (black) together. One important thing to remember while working with neopixel and additional power supply, ground should also go to Arduino. I faced this issues, neopixel was not working properly and it was because of that. That is why my 8 black wires were soldered into 2: one went to power supply and one to Arduino. 

When I connected all the clouds to power and ground I was able to program all of them fo different colors. All of them worked, however I would like to work more on the colors in particular. As of now each cloud has its own pin, there are enough of them surrently, but most probably something will be changed as we will be adding the Music Maker Shield. 

When all the neopixels were connected the Servo motor started lagging. This is a current issue we have to address. 
This is the current code:

<details>
<summary>Click to toggle contents of code</summary>

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
// SERVI PIN NUMBER 5
Servo myservo;

int pos = 100;  

int beginPos = 100;   // initial position of the servo
int targetPos = 115;   // target position of the servo
int step = 1;  // step size for each movement
unsigned long previousMillisMotor = 0;
const long interval_motor = 100;

const int IN1_PIN = 10; // the Arduino pin connected to the IN1 pin L298N
const int IN2_PIN = 2; // the Arduino pin connected to the IN2 pin L298N

const int IN3_PIN = 9; // the Arduino pin connected to the IN1 pin L298N
const int IN4_PIN = 8; // the Arduino pin connected to the IN2 pin L298N


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

    void setBlueValues(
      uint8_t _blueMinValue,
      uint8_t _blueMaxValue,
      uint8_t _blueCurrentValue,
      uint8_t _blueIncrementAmount)
    {
      blueMinValue = _blueMinValue;
      blueMaxValue = _blueMaxValue;
      blueCurrentValue = _blueCurrentValue;
      blueIncrementAmount = _blueIncrementAmount;
    }

    void setGreenValues(
      uint8_t _greenMinValue,
      uint8_t _greenMaxValue,
      uint8_t _greenCurrentValue,
      uint8_t _greenIncrementAmount)
    {
      greenMinValue = _greenMinValue;
      greenMaxValue = _greenMaxValue;
      greenCurrentValue = _greenCurrentValue;
      greenIncrementAmount = _greenIncrementAmount;
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
    if (pos >= targetPos || pos <= beginPos) {
      step *= -1; // Reverse direction when reaching target position or start position
    }
    myservo.write(pos);  // move the servo to the new position
  }
}


// pin, number of pixels, delay between steps
// front right
NeoPixelFader cloud1(A5, 20, 10); 
// back left
NeoPixelFader cloud2(A4, 20, 10);

NeoPixelFader cloud3(A3, 20, 10);

NeoPixelFader cloud4(A2, 20, 10);
NeoPixelFader cloud5(A1, 20, 10);
NeoPixelFader cloud6(A0, 20, 10);
NeoPixelFader cloud7(3, 20, 10);
NeoPixelFader cloud8(6, 20, 10);
void setup() {
  Serial.begin(9600);
  myservo.attach(5); 
  myservo.write(pos);
  // parameters are
  // redMinValue, redMaxValue, redCurrentValue,redIncrementAmount)
  //cloud1.setRedValues( 0, 20, 20, -1);
  cloud1.begin();
  cloud2.setRedValues( 10, 80, 10, -1);
  cloud2.begin();
  cloud3.setBlueValues(100, 200, 200, -1);
  cloud3.begin();
  cloud4.setBlueValues(70, 100, 100, -1);
  cloud4.begin();
  cloud5.setBlueValues(100, 200, 200, -1);
  cloud5.begin();
  cloud6.setGreenValues( 0, 50, 50, -1);
  cloud6.begin();
  cloud7.setBlueValues( 50, 100, 100, -1);
  cloud7.begin();
  cloud8.setGreenValues( 10, 50, 50, -1);
  cloud8.begin();

  pinMode(IN1_PIN, OUTPUT);
  pinMode(IN2_PIN, OUTPUT);  
  pinMode(IN3_PIN, OUTPUT);
  pinMode(IN4_PIN, OUTPUT);
}

void loop() {
  motor_check();
  cloud1.update();
  cloud2.update();
  cloud3.update();
  cloud4.update();
  cloud5.update();
  cloud6.update();
  cloud7.update();
  cloud8.update();
  motor_check();
  // back motor
  digitalWrite(IN1_PIN, HIGH); 
  digitalWrite(IN2_PIN, LOW); 
  // front motor
  digitalWrite(IN3_PIN, LOW);  
  digitalWrite(IN4_PIN, HIGH);
}
```
</details>


This is the video of our project on its current stage. 

https://github.com/lizadat/MachineLab/assets/98390904/8edd7379-a66e-4594-9946-7ece47c0bae3

The upcoming things:
- There was a chance to do the laser cutting, which involved laser cutting our cars and the city skyline, which we will attach to the bottom
- We need to troubleshoot the motor to have the smooth turning
- The Music Maker Shield is almost ready to be connected to the whole project, so we will continue working on it during the class on Wednesday
- As for the homework required: we have two power feeds ready and we just need to add the button and an LED, which will be relatevily easy to do. Also we will add the Music Maker Shield. 

