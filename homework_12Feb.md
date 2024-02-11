# Prototyping
We finalized our idea together with Ronit and started working on our parts separately.

### This is our final sketch for the project:
![image](https://github.com/lizadat/MachineLab/assets/98390904/db44c1a5-6109-4365-a0e2-064e83a02de3=500x500)

### Prototyping Process
I decided to create the moving part, which will hold the clouds. This part is supposed to be connected to the motor, which will rotate a few degrees one side and another lifting one side up and another down and vice versa. 

For prototyping I used the cardboard and hot glue as my primary tools. 
I cut the cardboard into 4 strips.
![1](https://github.com/lizadat/MachineLab/assets/98390904/c8c751bf-a4b5-4f02-9152-8c6af83e3192)

I knew that I would need to make the strips strong, so I glued two strips together and also added the wooden sticks inside for a better effect.
![IMG_3275](https://github.com/lizadat/MachineLab/assets/98390904/b7a7008b-960c-43a9-8f95-695023635c33)

After that I made another strip with the same metogology and glued everything together with an additional support - tape. As a result I had a 3-sided frame.
![3](https://github.com/lizadat/MachineLab/assets/98390904/19ca2c89-8d07-45b3-a7e1-d5245b3355c1)

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
![4](https://github.com/lizadat/MachineLab/assets/98390904/bbbc34dc-fb85-45ef-bff1-8aaf63c9c783)
![5](https://github.com/lizadat/MachineLab/assets/98390904/6b9430a8-d76a-4304-a43e-2757e60fe213)



