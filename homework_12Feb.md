# Prototyping
We finalized our idea together with Ronit and started working on our parts separately.

### This is our final sketch for the project:
<img src="https://github.com/lizadat/MachineLab/assets/98390904/db44c1a5-6109-4365-a0e2-064e83a02de3" width="50%" height="50%">

### Prototyping Process
I decided to create the moving part, which will hold the clouds. This part is supposed to be connected to the motor, which will rotate a few degrees one side and another lifting one side up and another down and vice versa. 

For prototyping I used the cardboard and hot glue as my primary tools. 
I cut the cardboard into 4 strips.

<img src="https://github.com/lizadat/MachineLab/assets/98390904/c8c751bf-a4b5-4f02-9152-8c6af83e3192" width="50%" height="50%">

I knew that I would need to make the strips strong, so I glued two strips together and also added the wooden sticks inside for a better effect.

<img src="https://github.com/lizadat/MachineLab/assets/98390904/b7a7008b-960c-43a9-8f95-695023635c33" width="50%" height="50%">

After that I made another strip with the same metogology and glued everything together with an additional support - tape. As a result I had a 3-sided frame.

<img src="https://github.com/lizadat/MachineLab/assets/98390904/19ca2c89-8d07-45b3-a7e1-d5245b3355c1" width="50%" height="50%">

I programmed the Servo motor to turn only 20 degrees one way and then 20 another with a longer delay - 50, so the movement is slower (I think it can be even more slower).
Here is the code:

#include <Servo.h>

Servo myservo; 

int pos = 0;  

void setup() {
  myservo.attach(9); 
}

void loop() {
  for (pos = 0; pos <= 20; pos += 1) {
    myservo.write(pos);            
    delay(50);                       
  }
  for (pos = 20; pos >= 0; pos -= 1) {
    myservo.write(pos);              
    delay(50);                       
  }
}

Then I attached the servo motor to the cardboard frame. I also had to use the tape and hot glue for a better connection:

<img src="https://github.com/lizadat/MachineLab/assets/98390904/bbbc34dc-fb85-45ef-bff1-8aaf63c9c783" width="50%" height="50%">

<img src="https://github.com/lizadat/MachineLab/assets/98390904/6b9430a8-d76a-4304-a43e-2757e60fe213" width="50%" height="50%">



Here is a [video1](https://drive.google.com/file/d/1Zsb3iwgc41TCGUlwi5kYZKgQE6IRgRRp/view?usp=sharing) and [video2](https://drive.google.com/file/d/1Zsb3iwgc41TCGUlwi5kYZKgQE6IRgRRp/view?usp=sharing) of how it looked in the progress!


Here are some takeaways from the prototyping process:
1. The frame should be very strong, even though it seems like there is not going to be a lot of weight on it. I plan to use the wood for it.
2. 3-sided frame will not be enough for stability, especially because it will be on height. So adding one more part on the other side will make it more stable and reliable.
3. I need to think of a stand for the motor and how to attach the motor to the stand.
4. How to attach the frame to the motor.

Those are the most concerning parts as of now. I hope to find the polyester stuffing so I can start working on the clouds itself. 


In the end me and Ronit put our prototypes together to see how it will look like. Here is what we have:

![7](https://github.com/lizadat/MachineLab/assets/98390904/575a0407-6e20-4e05-a68f-8e6ae4f32113)

For the ride part, done by Ronit, please refer to his [github page](https://github.com/rs7358/MachineLab/blob/main/homework_12Feb.md).

