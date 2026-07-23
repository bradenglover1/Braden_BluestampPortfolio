# Remote Control Car with Laser Turret
My project is a remote controlled car with a mounted laser turret. The car base is the Sunfounder car, while the mounted turret is made of 3D printed parts able to aim on 2 axes, controlled by 2 servo motors, with a laser attached as the weapon.


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Braden G | Berkeley High School | Civil Engineering | Incoming Senior

!(<img width="772" height="1022" alt="image" src="https://github.com/user-attachments/assets/7b508eaf-e32c-4904-adb8-cd69337d3143" />)
  
# Final Milestone
<iframe width="560" height="315" src="https://www.youtube.com/embed/mZH2pDb5PGI?si=6TCj-q0r3tglfHjh" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Explanation

My Final milestone was to download the code onto the car's R3 board and to get it working as a self driving car. I chose this because it was the last thing in my way before the base project would have been completed.

Challenges

One challenge I faced while getting the code onto the R3 board was the code not running correctly. I solved this problem by going through each error and adjusting accordingly until the project worked. The main problem was that some movement functions were using analogue movement, while others were using digital movement.

Next Steps

The 2 main next steps for me are, in order, 1. Change the total dependence on sensor movmeent, with remote controlled movements. The best option for this to my knowledge is the IR sensor and remote. 2. 3D print parts for attach a two axis laser pointer turret to the car, hopefully controlled remotly by a jystick, as well as adjust the wiring and circuitry organization on the car.


# Second Milestone


<iframe width="560" height="315" src="https://www.youtube.com/embed/U_TKEh0B1O8?si=ubsUrD8N63fN-T2N" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Explanation

My second milestone was to wire all of the modules together, so that when code is downloaded and run on the machine, nothing breaks or stops working.

Challenges

One Challenge I faced during this milestone was figuring out how the wiring system works on the car and deciding whether the videos or schematics were better to follow. I solved this problem by following the schematics, as they were clearer to follow than the videos.

Next Steps

The next thing that needs to be done is to write and download the code onto the R3 board of the car and to make sure that all sensors work properly with the code.
# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Explanation

My First Milestone was to acquire all parts for the car, which includes the 2 TT wheels, 1 Universal Wheel, 2 TT motors, the R3 board, L9110 Module, Ultrasonic Module, 2 IR obstacle Avoidance Modules, mini bread board, nuts and bolts to secure them, and wires to connect parts together. Along with Gathering all parts, I also needed to assemble them onto the base plate, so that the car can actually drive.

Challenges

One challenge that I faced when gathering and assembling the car was not having correctly sized screws to attach some modules. I solved this problem by asking around and finding replacement screws from the spare parts cabinet.

Next Steps

My plan after this is to wire all the parts together (Milestone 2), and download the self driving car code onto the R3 Board (final Milestone). 
  

# Starter Project

<iframe width="560" height="315" src="https://www.youtube.com/embed/TkALr4ICeYA?si=9RuQ742-VpvEKwKQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


Explanation

My starter project was the adjustable LED light. It consists of a circuit board, 3 sliders, each controlling the intensity of either red, green, or blue light on the LED, a USB-C adapter, and a multi-colored LED. The main goal of the project is to solder all of the parts to the circuit board in order to make the light color adjustable when powered. 

Challenges

the main challenge for me was remembering how to solder parts. Fortunatly, before I began this project, I was allowed to practice on a spare circuit board. Still, the first slider's soldering is rather mediocre. However, by the time I got to the third slider's soldering, the quality had improved drastically. 
  
# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here is the code that my car runs on
```
#include <Servo.h> // servo motor library
#include <IRremote.hpp> // IR remote library

//setting pins to different outputs, ie, IRreviever, wheel motors, servo motors.
const int IR_RECEIVE_PIN = 12; 
const int A_1B = 5;
const int A_1A = 6;
const int B_1B = 9;
const int B_1A = 10;
const int servoPinY = 3;
const int servoPinX = 2;
//creating X and Y axis servo objects
Servo servoY;
Servo servoX;  
//setting integer starting values
int x = 0; 
int y = 90;


void setup() {
    Serial.begin(9600);//communication channel for arduino uno board
    //attaching servos and sending them to starting positions
    servoY.attach(3);
    servoY.write(0);
    servoX.attach(2);
    servoX.write(90);
    //allow IR reviever to being recieving
    IrReceiver.begin(IR_RECEIVE_PIN, ENABLE_LED_FEEDBACK);  // Start the receiver
    Serial.println("REMOTE CONTROL START");
    //attach wheel motors
    pinMode(A_1B, OUTPUT);
    pinMode(A_1A, OUTPUT);
    pinMode(B_1B, OUTPUT);
    pinMode(B_1A, OUTPUT);
    delay(1000);
}
//function for moving forward using TT motors
void moveForward() {
    digitalWrite(A_1B, LOW);
    digitalWrite(A_1A, HIGH);
    digitalWrite(B_1B, HIGH);
    digitalWrite(B_1A, LOW);
}
//function for moving backwards using TT motors
void moveBackward() {
    digitalWrite(A_1B, HIGH);
    digitalWrite(A_1A, LOW);
    digitalWrite(B_1B, LOW);
    digitalWrite(B_1A, HIGH);
}
//same as above but right
void turnRight() {
    digitalWrite(A_1B, HIGH);
    digitalWrite(A_1A, LOW);
    digitalWrite(B_1B, HIGH);
    digitalWrite(B_1A, LOW);
}
//and left
void turnLeft() {
    digitalWrite(A_1B, LOW);
    digitalWrite(A_1A, HIGH);
    digitalWrite(B_1B, LOW);
    digitalWrite(B_1A, HIGH);
}
//function to stop all movement
void fullstop() {
    digitalWrite(A_1B, LOW);
    digitalWrite(A_1A, LOW);
    digitalWrite(B_1B, LOW);
    digitalWrite(B_1A, LOW);
}
//continuous loop for whole project
void loop() {
  //if the reciever recieves a button input from the IR remote, it prints the button ID 
  if (IrReceiver.decode()) {
    uint32_t key = IrReceiver.decodedIRData.command;
    Serial.println(key, HEX);
    //if key 2 is pressed(ID of 18), move forward
    if (key == 0x18) {//0x is before the ID because some ID's include letters, and 0x allows reading of letters and numbers
      moveForward();//calls function 
      Serial.println("HELLO");//says hello in console, to confirm action
      delay(10);
      }
    //if key 4 is pressed(ID of 8), turn left
    if (key == 0x8) {
      turnLeft();
      Serial.println("HELLO");
      delay(10);
      }
    //if key 6 is pressed(ID of 5a), turn right
    if (key == 0x5a) {
      turnRight();
      Serial.println("HELLO");
      delay(10);
      }
    //if key 8 is pressed(ID of 52), move backwards
    if (key == 0x52) {
      moveBackward();
      Serial.println("HELLO");
      delay(10);
      }
    //if key 5 is pressed(ID of 1c), stop
    if (key == 0x1c) {
      fullstop();
      Serial.println("HELLO");
      delay(10);
      }
    //if key - is pressed(ID of 15), aim laser upwards
    if (key == 0x15) {
      y=y+2;//add 2 to the Y integer
      servoY.write(y); //write the new Y angle to the servo
      Serial.print(" : ");
      Serial.print(y); //display new Y value in console
      Serial.print(" : ");
      }
    //same as above, but for key below -, and aims laser down
    if (key == 0x19) {
      y=y-2;
      servoY.write(y); 
      Serial.print(" : ");
      Serial.print(y); 
      Serial.print(" : ");
      }
    //same as above, but controls positive X axis on u/sd button
    if (key == 0x16) {
      x=x+2;
      servoX.write(x);
      Serial.print(" : ");
      Serial.print(x); 
      Serial.print(" : ");
      }
    //same as above, but controls negative x axis on 0 button
    if (key == 0xd) {
      x=x-2;
      servoX.write(x);
      Serial.print(" : ");
      Serial.print(x); 
      Serial.print(" : ");
      }
    IrReceiver.resume();  // Enable receiving of the next value   // Waits 1 second
  }
}
```
# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Sunfounder 3-in-1 starter kit | Contains car and all vanilla parts | $60 | https://www.amazon.com/SunFounder-Compatible-Tutorials-Including-Controller/dp/B0B778L1DZ/ref=sr_1_1_sspa?crid=1RKYNDFZFV9K5&dib=eyJ2IjoiMSJ9.D9LrCZJnua_keVMLJz2FWhhVJbiJ6dlnOqZ4gzJikw0.Y29jV-luir_nypOKQWGuCDlusQMU0MDZTq49-3jb74M&dib_tag=se&keywords=sunfounder+3+in+1%5C&qid=1784677123&s=electronics&sprefix=sunfounder+3+in+%2Celectronics%2C219&sr=1-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1> Link |
|SG90 micro servo motors|for X and Y control of laser turret|$5| https://www.amazon.com/Control-Raspberry-Helicopter-Airplane-Controls/dp/B0DFKPVRC2/ref=sims_dp_d_dex_ai_rank_model_1_d_v1_d_sccl_1_1/134-0101285-2033115?pd_rd_w=48nMP&content-id=amzn1.sym.bb4a0aac-c2b4-4b4b-a0c8-9aa89b28dce3&pf_rd_p=bb4a0aac-c2b4-4b4b-a0c8-9aa89b28dce3&pf_rd_r=RXZXS6B960NGGP7WQ2N1&pd_rd_wg=KKpnf&pd_rd_r=0d3aa9fa-b88f-4bcb-a46d-a6a3a7dd4c6c&pd_rd_i=B0DFKPVRC2&th=1 |
| 6 AA battery holder | for holding batteries for car | $8 (3 units) | https://www.amazon.com/LAMPVPATH-Pack-Battery-Holder-Leads/dp/B07KVJ9FPN/ref=sr_1_4?dib=eyJ2IjoiMSJ9.gE9JrlvyjIIMPFtNhpZMnvqqG9WudRZlN4cDhcYDGTx-s4iu7w4NSW7BE7j3qQUz_okidbFnD5_bUuMA8xtGiND5b47cuhLDnufNUk6AZ_zxYbLtj_vFx67pj8YcaD0bxDcfiW-nPHa2q4hfwCQ1kx3fA3VIG4m_cKfqlWn-dI2AL-z4KJDeKg5oO5fe-xBSIszCWrO4RMcI3gHJskGXm3YyKOZ16S6nKQybJJ_MA48.N1Mt7vJay_rvT3eUBfy9uk4s18cViWmOcaW-YuXQJbo&dib_tag=se&keywords=6+aa+battery+pack&qid=1784842424&sr=8-4 |
| 6 AA batteries | 9 Volts of power | $7.61 | https://www.amazon.com/Coppertop-Batteries-Ingredients-Long-lasting-Household/dp/B000IZQO7U/ref=sr_1_5?crid=SWSC123S74T4&dib=eyJ2IjoiMSJ9.Z-T-vAyHiXzMwwnyQViS8qQ8pt1pDDm2NOHHtWUNjk0dTqoyTHxxgvU2pJfok-ia_nXejGcJUKIXgpQDP67oektWkRdjGR7kvkl8Uddht9e4wy2KeQp2UJIqTtOXqPCbzOMTkI8MlqF-tvoRDrW0a4wjv3MdfUuqb_gMgVTdvpGr1-YRX81Ko4Gwpb1rLbJQlA1vx45qDi7E9NemJ5dphX5XTfmUmSemOoYreI2IOluO31n3q669iNcI-vdxvMpdn8kqRc1NHQkLSXl6om8MmGJxFUSu-IiyP8IOerMgMDY.V8jWfl53i-0aiXrwcSC7-JXxaKi2JEQeDVvB7UsODgI&dib_tag=se&keywords=6%2Baa%2Bbattery&qid=1784842576&sprefix=6%2Baa%2Bbattery%2Caps%2C236&sr=8-5&th=1 |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
