# Proccess documentation

This weekend I continued working on my sky part for the skyride.
Here is what I have done:

1. I started with sawing the right size wood. I measured the length, width and height of our base for the clock and 
decided how long wood sticks should be to fit in.
<img src="https://github.com/lizadat/MachineLab/assets/98390904/9e8baf6d-3458-49a8-8c26-2743046dd187" width="50%" height="50%">

3. I put the sticks together to see how it will look like and then attached them to each other with the screws.
The first screw did not go that well (cause I do not have a lot of experience with that), but the rest were pretty well.
<img src="https://github.com/lizadat/MachineLab/assets/98390904/ecff300f-f64b-4f03-85bb-0ab38b0a7aea" width="50%" height="50%">
<img src="https://github.com/lizadat/MachineLab/assets/98390904/2475cde9-c397-48c1-b667-65f158e6a9c3" width="50%" height="50%">

4. In order to attach the rotational part of the motor to the frame I attached the special bracing to it also with the help
of the screws. I realized that my wood stick is quite narrow, so I could not attach it all around and used just 4
screws instead of 8.
<img src="https://github.com/lizadat/MachineLab/assets/98390904/1b4989b0-1dc6-4c57-b963-cb275fc5f94b" width="50%" height="50%">

5. Then I worked with two stands, one of which will hold the motor. I attached the metal holders to the top of one stand with the screws and used the 4M bolts to attach the motor
<img src="https://github.com/lizadat/MachineLab/assets/98390904/d94dfbda-63bf-4694-abde-3b721c197f4b" width="50%" height="50%">
<img src="https://github.com/lizadat/MachineLab/assets/98390904/6435b811-b727-4f83-90c2-648c1f22490b" width="50%" height="50%">

6. These are all components I worked with. They cannot be dissambled, so if I want to change something I would have to do everything again. When I attached the motor I realized that it became higher than it was supposed to be, so I ended up doing some more sawing of the stand, which hold the motor.
<img src="https://github.com/lizadat/MachineLab/assets/98390904/655a4a51-ed67-4c0d-9d66-48d97409061e" width="50%" height="50%">

7. To try out I attached the motor and the frame to see how it will look like. 
<img src="https://github.com/lizadat/MachineLab/assets/98390904/13acaed1-5678-4169-8ba7-733a2f7a13ab" width="50%" height="50%">

8. In the other stand I drilled a whole and placed something similar to bolt. I also drilled one side of the frame and then the bolt went in there
as well. I did not fix it, because it serves more as just a support. Here is how it looked like:
<img src="https://github.com/lizadat/MachineLab/assets/98390904/a814fc6d-07f8-4c90-9666-d85e2f430a3b" width="50%" height="50%">

10. Then I was able to put all the parts together and make everything stand. 
<img src="https://github.com/lizadat/MachineLab/assets/98390904/e401002d-7ce7-42f0-81de-60c87a551eeb" width="50%" height="50%">
<img src="https://github.com/lizadat/MachineLab/assets/98390904/df8f34a3-3646-49f7-b4b0-be5024cf409a" width="50%" height="50%">

11. Then I started working on the other part: the clouds. For that I did soldering first to connect the neopixel with the wires (I made a huge mistake first by soldering the red wire to ground and black to 5V...).
![1](https://github.com/lizadat/MachineLab/assets/98390904/8e01000c-d939-4085-bb02-a6e30753d030)

12. The I wrote a simple code to control the LEDs, but I would like to change it to make it as a gradient.
Here is a code (I edited the sample from the Neopixel librart):
#include <Adafruit_NeoPixel.h>
#ifdef __AVR__
 #include <avr/power.h>
#endif

#define PIN        5
#define NUMPIXELS 33 

Adafruit_NeoPixel pixels(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

#define DELAYVAL 50 

void setup() {
#if defined(__AVR_ATtiny85__) && (F_CPU == 16000000)
  clock_prescale_set(clock_div_1);
#endif

  pixels.begin(); 
}

void loop() {
  int blue_val = random(0, 255);
  for(int i=0; i<NUMPIXELS; i++) { // For each pixel...
    pixels.setPixelColor(i, pixels.Color(0, 0, blue_val));
    pixels.show(); 
    delay(DELAYVAL);
  }
}
![2](https://github.com/lizadat/MachineLab/assets/98390904/748a0730-2faa-42f1-896c-57d4fe48dd81)

13. After that I used the polyester stuffing to create a cloud around it. I also used hot glue to stick the material and fill the gaps.
![3](https://github.com/lizadat/MachineLab/assets/98390904/9b0bd07a-3c18-48a8-98f0-2e7cca8f569a)


14. When I connected all the wires and put the LEDs in the cloud here is what I've got:










