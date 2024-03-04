# Project progress

### PROGRESS IN CLASS
Ronit 3D printed the car we plan to use for our sky ride. 
It was supposed to be easily assembled, however we faced an issues. The parts were supposed to be constructed together (similar to LEGO), but it did not work as printed parts, holes were not exactly the right size. So we ended up using a glue for plastic to put all the pieces together. It was pretty strong, the glue did good job, but it took us quite a long time in comparison to what it could be if the printing was the way it was supposed to be. 


<img src="https://github.com/lizadat/MachineLab/assets/98390904/5b293370-aa3a-4d93-9881-6f22196064c1" width="50%" height="50%">


<img src="https://github.com/lizadat/MachineLab/assets/98390904/36c6b5d9-a394-4b85-b6db-3a053ac4f2b2" width="50%" height="50%">


We also did a lot of planning in terms of all right measurements for our ride and frame for a final look. We faced a few issues, for example we had to make sure that the stand for a sky frame and the car do not touch each other, the car does not collide with a vertical plane on the back and so on. We could draw everything on our draft bottom, which helped a lot. 


<img src="https://github.com/lizadat/MachineLab/assets/98390904/41c7d7df-14e6-4692-be98-9e777827f701" width="50%" height="50%">


As a result here are some important measurements: the stands for a frame should be 75 cm high, this is where the frame will be attached. The size of a frame 43*34 (as far as I can remember) cm. @michaelshiloh helped us to cut the aluminium pieces the right length, so that the work is done better and faster.


<img src="https://github.com/lizadat/MachineLab/assets/98390904/5b21a37e-6a67-4fbf-8eef-8492e609c793" width="50%" height="50%">


Our plan for the future was:
- Cut the metal for the ride stands
- Create (assemble) the stands
- Make the pillar for the ride
- One more or two more clouds
- Decide on the rope (try out the fishing line 1 mm)


### PROGRESS AT HOME

WORKING WITH METAL
I was first quite scared about working with metal, cause drilling and everything looked much harder than with wood. However, as a result I enjoyed the process and learned how to do everything.

Just when I started figuring out where to drill the holes I had a dilemma. My plan was to drill the holes in the middle and on both sides, so that I would used one bolt to connect the angle brackets on both sides. However, the brackets I used had the holes in different places and even when I tried to connect them with one bolt, the brackets would appear tilted, so this method did not work.


<img src="https://github.com/lizadat/MachineLab/assets/98390904/5454df79-eb1c-4d63-af02-0a9565c84243" width="50%" height="50%">


I used a used metal pieces to figure out the right connection I wanted to use. I was advised to use a screw to connect the brackets and have 2 screews on each side. I thought they would obstruct one another, but surprisingly the did not, and it all was quite tight. 


<img src="https://github.com/lizadat/MachineLab/assets/98390904/b574f06d-d02e-4d0a-b76e-c51a761d0f6b" width="50%" height="50%">


So I used this method for my initial metal part. I also marked all other spots for the holes for the frame and drilled. After that I connected the motor to one of my stands and I really liked how strong it was. I feel that motor is quite heavy and the stand, with two brackets on the opposite sides were not enough. What I did is that on the other stand the two brackets are not on the other sides as in the first stand, so they can support the motor from falling to the sides. 


<img src="https://github.com/lizadat/MachineLab/assets/98390904/e3f7bd57-cc9e-4009-be12-a3079f220cd6" width="50%" height="50%">


When I assembled the frame it was very loose. I do not know what might be the reason, but I have 2 ideas: 1 - I need to tight more the bolts and nuts; 2 - there are small pieces of metal left on the holes after drilling, so maybe I need to find a specific tool which can remove them. 


Even though the frame was quite loose I still tried to connect it to the stands and see how it was. I really like that it doesn't take much space, but is very strong. However, I do need to make sure that everything is very tight. 

<img src="https://github.com/lizadat/MachineLab/assets/98390904/af64566b-615d-4e8f-a099-02732b3bdf43" width="50%" height="50%">


https://github.com/lizadat/MachineLab/assets/98390904/f7aff5da-c223-405f-8b47-55289b33864c


After advising with the professor I fixed the frame. I used a metal file to remove the pieces left on the frame parts after the drilling. I think because I had some of them left there it prevented the nut from a complete tightness. Moreover, I was shown where the proper tools were for tightening the nuts, so as a result I used them and everything turned out the way I planned. 

After that I proceeded with installing my metal construction to the wooden bottom.
I measured where the stands were supposed to be and drilled the holes and used the screws to attach the stands to the bottom. 
They stood very firm. 


<img src="https://github.com/lizadat/MachineLab/assets/98390904/c6a3025f-2486-4d7b-b7ae-add3f094762f" width="50%" height="50%">



After that I added the frame. I am glad that with the bolts it is relatively easy to assemble and disassemble everything, so I can easily take the frame down. Everything seems very steady and I like it.


<img src="https://github.com/lizadat/MachineLab/assets/98390904/1ae884db-9dc2-45b0-9d1e-2bb24a0b12c7" width="50%" height="50%">



My next step was to set up the right degrees values for the motor. I again used a potentiometer to find out the values, because when I attached the frame it was in a different place then I had before. Now the degrees I use are 95-115. 

<details>
<summary>Click to toggle contents of code for the motor with new degree values</summary>

```
#include <Servo.h>

Servo myservo; 

int pos = 0;  

void setup() {
  myservo.attach(9); 
  myservo.write(pos);
}

void loop() {
  for (pos = 95; pos <= 115; pos += 1) {
    myservo.write(pos);   
             
    delay(100);                       
  }
  for (pos = 115; pos >= 95; pos -= 1) {
    myservo.write(pos);              
    delay(100);                       
  }
}
```
</details>

<img src="https://github.com/lizadat/MachineLab/assets/98390904/5bfab3c3-004f-46c4-b173-b8471fb352da" width="50%" height="50%">



Being curious I attached the clouds with the tape to the frame. I wanted to see the whole picture of my work and I think with the clouds it looks very cute. I realized that the wires that go from the clouds should be longer, but I will solder more when I know exactly where the Arduino will be placed. I also Think that the middle is quite empty, so most probably I will add some crossing in between so I can add more clouds there. 

<img src="https://github.com/lizadat/MachineLab/assets/98390904/63f27617-141e-4b77-bbac-44cb76077fec" width="50%" height="50%">


Here is the final result from my work over this week:

https://github.com/lizadat/MachineLab/assets/98390904/996b0ff1-07b3-4e21-8ee6-c2a0cb465f37





My plan for the future:
- I want to make a few mor clouds and connect them to my frame
- Maybe, have everything connected (clouds and motor) and see how the whole picture looks like.

We will also continue working on our sky ride. Go to the [Ronit's github](). 



