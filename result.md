# Result

We finally finished our project - Theme Park!

We had 5 separate projects which were combined into 2. 

Here are the videos and pictures to remember!

As how most of the time it happens we were working last minute to fix some issues, but our brilliant professor made it all work!

<img src="https://github.com/lizadat/MachineLab/assets/98390904/cdf5a7e9-e9a7-4422-a1f1-9710bcf1d9c0" width="50%" height="50%">


Here is our SkyRide (Cable car) installed in the frame and next to other projects!

<img src="https://github.com/lizadat/MachineLab/assets/98390904/2a96116f-ce6e-45d5-87d2-33d08116e7f4" width="50%" height="50%">


And me next to my project excited to press the YELLOW button to start it off!

<img src="https://github.com/lizadat/MachineLab/assets/98390904/665d508f-6954-4636-97aa-2de6e0cb3f5c" width="50%" height="50%">


We had to [move](https://youtube.com/shorts/FLdX-pwgpzU) our frame through the whole lobby and it was very fun, because it attracted many people! The frame is huge and nobody expected to see something like this! We gathered a big crowd on our way and brought them to the [opening](https://youtube.com/shorts/WuPb5EbwdrU)!
Here is the [video](https://youtube.com/shorts/pLpD_HR3fa8?feature=share) of all projects. 


Here is also our final code for both Arduinos:

<details>
<summary>Click to toggle contents of code for main Arduino</summary>

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

//#include <Servo.h>
#include <Adafruit_NeoPixel.h>
// SERVI PIN NUMBER 5
//Servo myservo;
#define LED_PIN    7

// How many NeoPixels are attached to the Arduino?
#define LED_COUNT 76
Adafruit_NeoPixel strip(LED_COUNT, LED_PIN, NEO_GRB + NEO_KHZ800);
//int pos = 100;  

// Pins for communicating with the master clock
const int triggerPin = 4;  // triggers this activity
bool triggerPinState = false;
const int donePin = 11;      // signals that I'm done
bool donePinState = true;


// int beginPos = 100;   // initial position of the servo
// int targetPos = 115;   // target position of the servo
// int step = 1;  // step size for each movement
//unsigned long previousMillisMotor = 0;
//const long interval_motor = 100;

unsigned long currentMillisSystem = millis();
unsigned long previousMillisSystem = 0;
const long interval_system = 25000;

const int IN1_PIN = 10; // the Arduino pin connected to the IN1 pin L298N
const int IN2_PIN = 2; // the Arduino pin connected to the IN2 pin L298N

const int IN3_PIN = 9; // the Arduino pin connected to the IN1 pin L298N
const int IN4_PIN = 8; // the Arduino pin connected to the IN2 pin L298N

void colorWipe(uint32_t color) {
  for(int i=0; i<strip.numPixels(); i++) { // For each pixel in strip...
    strip.setPixelColor(i, color);         //  Set pixel's color (in RAM)
    strip.show();                          //  Update strip to match
  }
}

void clearAll(int numberOfPixels){
  for (int i = 0; i < numberOfPixels; i++) {
      strip.clear();
      strip.show();
    }
}

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

    void clear(int numberOfPixels){
      for (int i = 0; i < numberOfPixels; i++) {
          pixels.clear();
          pixels.show();
        }
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

// void motor_check(){
//   unsigned long currentMillisMotor = millis();  // get the current time
//   // check if it's time to move the servo
//   if (currentMillisMotor - previousMillisMotor >= interval_motor) {
//     previousMillisMotor = currentMillisMotor;

//     // move the servo towards the target position
//     pos += step;
//     if (pos >= targetPos || pos <= beginPos) {
//       step *= -1; // Reverse direction when reaching target position or start position
//     }
//     myservo.write(pos);  // move the servo to the new position
//   }
// }


// pin, number of pixels, delay between steps
NeoPixelFader cloud1(A5, 20, 10); 
NeoPixelFader cloud2(A4, 20, 10);
NeoPixelFader cloud3(A3, 20, 10);
NeoPixelFader cloud4(A2, 20, 10);
NeoPixelFader cloud5(A1, 20, 10);
NeoPixelFader cloud6(A0, 20, 10);
NeoPixelFader cloud7(3, 20, 10);
NeoPixelFader cloud8(6, 20, 10);

void setup() {
  Serial.begin(9600);
  strip.begin();
  strip.show();
  // myservo.attach(5); 
  // myservo.write(pos);
  pinMode(donePin, OUTPUT);
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
  unsigned long currentMillisSystem = millis();  // get the current time
  if(donePinState == true){
    digitalWrite(donePin, HIGH);
  }
  if (digitalRead (triggerPin) == HIGH) {
    Serial.println("Button pressed!");
    previousMillisSystem = currentMillisSystem;
    triggerPinState = true;
    donePinState = false;
  }
    if(donePinState == false){
      digitalWrite (donePin, LOW);
      Serial.println("EVERYTHING RUNNING");
      // giant servo motor
      //motor_check();
      colorWipe(strip.Color(255,   248,   194)); // yellow
      // neopixels
      cloud1.update();
      cloud2.update();
      cloud3.update();
      cloud4.update();
      cloud5.update();
      cloud6.update();
      cloud7.update();
      cloud8.update();

      // back motor
      digitalWrite(IN1_PIN, HIGH); 
      digitalWrite(IN2_PIN, LOW); 
      // front motor
      digitalWrite(IN3_PIN, HIGH);  
      digitalWrite(IN2_PIN, LOW);
    if (currentMillisSystem - previousMillisSystem >= interval_system) {
      Serial.println("EVERYTHING STOPPED");
      donePinState = true;
      for (int i = 0; i < LED_COUNT; i++) {
        strip.clear();
        strip.show();
      }
      // neopixels
      cloud1.clear(20);
      cloud2.clear(20);
      cloud3.clear(20);
      cloud4.clear(18);
      cloud5.clear(20);
      cloud6.clear(20);
      cloud7.clear(20);
      cloud8.clear(20);
     

      // back motor
      digitalWrite(IN1_PIN, LOW); 
      digitalWrite(IN2_PIN, LOW); 
      // front motor
      digitalWrite(IN3_PIN, LOW);  
      digitalWrite(IN4_PIN, LOW);
    }
    }
  }
```
</details>


<details>
<summary>Click to toggle contents of code for additional Arduino</summary>

```
#include <SPI.h>
#include <Adafruit_VS1053.h>
#include <SD.h>

// Pin definitions (same as your provided code)
#define SHIELD_RESET  -1
#define SHIELD_CS     7
#define SHIELD_DCS    6
#define CARDCS 4
#define DREQ 3

Adafruit_VS1053_FilePlayer musicPlayer = 
Adafruit_VS1053_FilePlayer(SHIELD_RESET, SHIELD_CS, SHIELD_DCS, DREQ, CARDCS);


#include <Servo.h>
// SERVO PIN NUMBER 5
Servo myservo;
int pos = 100; 

unsigned long previousMillisMotor = 0;
const long interval_motor = 100;
int beginPos = 100;   // initial position of the servo
int targetPos = 115;   // target position of the servo
int step = 1;  // step size for each movement

// Pins for communicating with the master clock
const int triggerPin = 8;  // triggers this activity - green
bool triggerPinState = false;
bool donePinState = true;

// main clock
unsigned long currentMillisSystem = millis();
unsigned long previousMillisSystem = 0;
const long interval_system = 45000;

void motor_check(){
unsigned long currentMillisMotor = millis();  // get the current time
//Serial.println("MOTOR ACTIVATED");
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

// Function to play a track based on its number
void playNextTrack(int trackNumber) {
  char filename[15];
  sprintf(filename, "/track00%d.mp3", trackNumber);
  Serial.print(F("Playing "));
  Serial.println(filename);
  musicPlayer.startPlayingFile(filename);
}

void setup() {
  Serial.begin(9600);
  myservo.attach(5); 
  myservo.write(pos);
  Serial.println("Adafruit VS1053 Simple Test");

  if (!musicPlayer.begin()) {
    Serial.println(F("Couldn't find VS1053, do you have the right pins defined?"));
    while (1);
  }
  Serial.println(F("VS1053 found"));

  if (!SD.begin(CARDCS)) {
    Serial.println(F("SD failed, or not present"));
    while (1);
  }

  musicPlayer.setVolume(1,1);
  musicPlayer.useInterrupt(VS1053_FILEPLAYER_PIN_INT);
}

void loop(){

  unsigned long currentMillisSystem = millis();  // get the current time
  if (digitalRead (triggerPin) == HIGH) {
    Serial.println("Button pressed!");
    previousMillisSystem = currentMillisSystem;
    triggerPinState = true;
    donePinState = false;
  }

  if(donePinState == false){
    motor_check();
    if (musicPlayer.stopped()) {
      static int trackNumber = 1;  // keep track of which song to play next
      trackNumber++;
      if (trackNumber > 2) {
        trackNumber = 1;  // wrap around to the first track
      } 
      motor_check(); 
      playNextTrack(trackNumber);
      motor_check(); 
    }

    if (currentMillisSystem - previousMillisSystem >= interval_system) {
        //Serial.println("EVERYTHING STOPPED");
        musicPlayer.stopPlaying();
        donePinState = true;
    }
  }
}
```
</details>
