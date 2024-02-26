# Process Documentation

Collaboration with [Ronit](https://github.com/rs7358/MachineLab/blob/main/homeword_26Feb.md). The sky ride part is on his guthub page.

### In class work:

Since we had time in class to work on our project, I and Ronit connected the frame with the stands to the bottom.
First we sawed the necessary pieces for both stands:


<img src="https://github.com/lizadat/MachineLab/assets/98390904/22649fc7-54f6-4681-ab79-731896549b5e" width="50%" height="50%">



Secondly we connected the stands with the frame to the bootom with the screws. It is good that there were two of us, becuase one person held 
a stand with a frame and another used a drill and then screws to connect.


<img src="https://github.com/lizadat/MachineLab/assets/98390904/a275ae63-10ed-456e-882e-1d81ef40c07e" width="50%" height="50%">


<img src="https://github.com/lizadat/MachineLab/assets/98390904/34dc1890-59f9-415c-bf90-c88ddbe3b8f6" width="50%" height="50%">



After connecting everything here is what we received. The conncetion seemed to be very strong.


<img src="https://github.com/lizadat/MachineLab/assets/98390904/211fe23e-46b8-43fc-96a9-3cf44daac9a4" width="50%" height="50%">



Here is an overall view, how we plan it to look like in the future.


<img src="https://github.com/lizadat/MachineLab/assets/98390904/0238786d-cdc3-4376-901c-b4b7c9db9b89" width="50%" height="50%">



Next step: to find out the right degrees values for a proper movement of the frame.


<img src="https://github.com/lizadat/MachineLab/assets/98390904/ab5cec7f-bd9b-4594-890c-be41d956cb1b" width="50%" height="50%">



Some decisions made in class:
- We will use aluminuim for our final look, so it means that I have to start working with metal.
- The motor will now be placed vertically instead.
- We will first work on the ride and then do the frame which will correspond in the size.

### Homework

I started with creating the scheme on paper for the motor plate to hold the motor and connect to the stand.
I first drew it on paper with all the necessary measurements and then for a better understanding made a digital version:


<img src="https://github.com/lizadat/MachineLab/assets/98390904/c85800d0-078e-4c8f-a496-8c485a78efef" width="40%" height="40%">


<img src="https://github.com/lizadat/MachineLab/assets/98390904/0b3a751b-c982-449a-a03f-3b57c4a03400" width="40%" height="40%">


Thanks to @michaelshiloh the motor plate was made. It prefectly fitted the motor, so I am very glad. The only thing - I could do only 4mm wholes for the bolts, for some reason I thought it was 5. But it all holds together perfectly. 


<img src="https://github.com/lizadat/MachineLab/assets/98390904/14a5c5cb-57b5-4c16-b0b1-2d263842bfc7" width="50%" height="50%">



Before I faced the problem where I could not figure out the right degrees values for a proper frame turn. So after attached the motor plate and connecting the motor to the power and also adding the potentiometer I figured everythign out:
I need the motor to start at 16 degrees and then rotate + and - 10, which is 6 and 26. It can be less, depending on how big the frame will be. 


<img src="https://github.com/lizadat/MachineLab/assets/98390904/cd54ffbd-c60f-4f66-b382-b54a8d909f51" width="50%" height="50%">



<details>
<summary>Click to toggle contents of code for potentiometer and Servo motor </summary>

```
#include <Servo.h>

Servo myservo;  // create servo object to control a servo

int potpin = A0;  // analog pin used to connect the potentiometer
int val;    // variable to read the value from the analog pin

void setup() {
  Serial.begin(9600);
  myservo.attach(9);  // attaches the servo on pin 9 to the servo object
}

void loop() {
  val = analogRead(potpin);            // reads the value of the potentiometer (value between 0 and 1023)
  val = map(val, 0, 1023, 0, 180);     // scale it for use with the servo (value between 0 and 180)
  Serial.println(val);
  myservo.write(val);                  // sets the servo position according to the scaled value
  delay(15);                           // waits for the servo to get there
}

```
</details>


As we decided to do the final set up with aluminum I decided to practice working with it.
I first cut a piece 45 cm long, which can potentially be a part of the frame. I ended up cutting it like 30 degrees to one side and I do not know why. It was not straight, but it is ok. For the future I would like to use some special machine for cutting metal, so that everything is straight and looks nice. 

I had to drill two holes in this piece, but the trick was that it had to be very very precise to fit the motor connector. Unfortunately I did not do well so I had to somehow make a hole 1-2 mm to one side, which took quite a long time.


<img src="https://github.com/lizadat/MachineLab/assets/98390904/0bec5432-0d3a-481c-ac20-138270b10b94" width="50%" height="50%">



But, I manage to connect it with bolts. It has quite a strong connection even though it is only 2 bolts out of 6. I do not know whether it will be enough or I would have to think of how to connect the rest, because that piece of metal is not wide. 


<img src="https://github.com/lizadat/MachineLab/assets/98390904/075fa439-9a79-4528-8ceb-96a02cb930d4" width="50%" height="50%">



CLOUDS (my most exciting thing):
For this week I wanted to write the right code for what I wanted: the light blue - dark blue - dark purple gradient.
I found some example on the Arduino Help Forum. Here is a [webpage](https://forums.adafruit.com/viewtopic.php?t=122440) I used as a source. It took me some time to figure out how the code worked, but as soon as I did I understood the whole idea and was able to do 3 different colors change!

Here is the result:


<img src="https://github.com/lizadat/MachineLab/assets/98390904/9e4498a8-f083-43c9-b904-d7ae468a21ea" width="50%" height="50%">


Video:

https://github.com/lizadat/MachineLab/assets/98390904/2e37a97e-998b-4447-b3a3-52722a78701e


<details>
<summary>Click to toggle contents of code for the gradient</summary>

```
#include <Adafruit_NeoPixel.h>
#define PIN 5
#define NUMPIXELS 33
Adafruit_NeoPixel pixels = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

void setup()  {
  pixels.begin();
  pixels.show();
  Serial.begin(9600);
}

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
}
```
</details>


In order to make some more progress this week I decided to create two additional clouds.
When we tried putting clouds in our whole composition, the cloud was quite big. I had 33 neopixels in there, so this time I made one 18 and another 20 pixels. 

I started with cutting the neopixels strip and soldering. This time I already knew how to do it in easy way, so the soldering turned out much nicer and I did it faster. 


<img src="https://github.com/lizadat/MachineLab/assets/98390904/e1bcd849-e52e-4484-bcdf-76af4e4945f7" width="50%" height="50%">



To fix the neopixels in the way I wanted I used small plastic ties and created a small bow. 


<img src="https://github.com/lizadat/MachineLab/assets/98390904/0b16dab6-ea2d-448e-a774-86c9eab6b40b" width="50%" height="50%">




The last step included adding the polyester stuffing. This time I directly glued it with hot glue to the neopixel strip and not like the last time (created a 'bag' and put the strip in it). I figured out that it was not very reliable and there were many holes. This was of just direct gluing was much better.



<img src="https://github.com/lizadat/MachineLab/assets/98390904/24eb211c-033c-4dc4-8949-7c001d153178" width="50%" height="50%">



What will I get done for next week?
- I will connect the freshly made clouds and see if it works. I would like to also change the colors, so that all of them have different shades.
- I will start building the frame and the stands for it.
- I will also connect it to the motor and make a proper rotation
- We will continue working on the ride itself. I think we will created a wood or maybe the metal stand for the motors and will improve in our design of the cars. 


