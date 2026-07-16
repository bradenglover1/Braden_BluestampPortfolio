# Remote Control Car with Laser Turret
My project is a remote controlled car with a mounted laser turret. The car base is the Sunfounder car, while the mounted turret is a 3D printed able to aim on 2 axes. My biggest challenge has been making code work, because I have very little experience with coding. A big takeaway for me was ... . (triumph). 


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Braden G | Berkeley High School | Civil Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone
<iframe width="560" height="315" src="https://www.youtube.com/embed/mZH2pDb5PGI?si=6TCj-q0r3tglfHjh" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

My third milestone was to download the code onto the car R3 board. My biggest challenge at BSE was figuring out the arduino coding parts of the assembly. I solved this problem by rewriting the code for the self driving car, which eventually made the code run smoothly. Some key topics I learned about were the aforementioned arduino coding, as well as wiring of the car's components. Things I hope to learn more about in the future is self making circuitry/wiring components together.


# Second Milestone


<iframe width="560" height="315" src="https://www.youtube.com/embed/U_TKEh0B1O8?si=ubsUrD8N63fN-T2N" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

  My second milestone was to wire all of the modules together, so that when code is downloaded and run on the machine, nothing breaks or stops working.  One Challenge I faced during this milestone was figuring out how the wiring system works on the car. The next thing that needs to be done is to write and download the code onto the R3 board of the car and to make sure that all sensors work properly with the code.
# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My First Milestone was to acquire all parts for the car, which includes the 2 TT wheels, 1 Universal Wheel, 2 TT motors, the R3 board, L9110 Module, Ultrasonic Module, 2 IR obstacle Avoidance Modules, mini bread board, nuts and bolts to secure them, and wires to connect parts together. Along with Gathering all parts, I also needed to assemble them onto the base plate, so that the car can actually drive.'
One challenge that I faced when gathering and assembling the car was not having correctly sized screws to attach some modules. I solved this problem by asking around and finding replacement screws from the spare parts cabinet.
My plan after this is to wire all the parts together (Milestone 2), and download the self driving car code onto the R3 Board (final Milestone)
  

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
const int A_1B = 5;
const int A_1A = 6;
const int B_1B = 9;
const int B_1A = 10;
const int rightIR = 7;
const int leftIR = 8;
const int trigPin = 3;
const int echoPin = 4;

void setup() {
    pinMode(A_1B, OUTPUT);
    pinMode(A_1A, OUTPUT);
    pinMode(B_1B, OUTPUT);
    pinMode(B_1A, OUTPUT);
    pinMode(echoPin, INPUT);
    pinMode(trigPin, OUTPUT);
}
void moveForward(int speed) {
    analogWrite(A_1B, 0);
    analogWrite(A_1A, speed);
    analogWrite(B_1B, speed);
    analogWrite(B_1A, 0);
}
void moveBackward(int speed) {
    digitalWrite(A_1B, speed);
    digitalWrite(A_1A, 0);
    digitalWrite(B_1B, 0);
    digitalWrite(B_1A, speed);
}
void backLeft(int speed) {
    analogWrite(A_1B, speed);
    analogWrite(A_1A, 0);
    analogWrite(B_1B, 0);
    analogWrite(B_1A, 0);
}
void backRight(int speed) {
    analogWrite(A_1B, 0);
    analogWrite(A_1A, 0);
    analogWrite(B_1B, 0);
    analogWrite(B_1A, speed);
}
float readSensorData() {
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    float distance = pulseIn(echoPin, HIGH) / 58.00; //Equivalent to (340m/s*1us)/2
    return distance;
}

void loop() {

    int left = digitalRead(leftIR);   // 0: Obstructed  1: Empty
    int right = digitalRead(rightIR);

    if (!left && right) {
        backLeft(150);
    } else if (left && !right) {
        backRight(150);
    } else if (!left && !right) {
        moveBackward(150);
    } else {
        float distance = readSensorData();
        Serial.println(distance);
        if (distance > 50) { // Safe
            moveForward(200);
        } else if (distance < 10 && distance > 2) { // Attention
            moveBackward(200);
            delay(1000);
            backLeft(150);
            delay(500);
        } else {
            moveForward(150);
        }
    }
}
```
# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Sunfounder R3 Board | Runs code for the car | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| L9110 Motor Driver Module | Controls motor functions/coordination | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| TT Motor | Motors to make wheels spin | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Ultrasonic Module | Constantly checks for the distance between it and any object ahead | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Obstacle Avoidance Module | Constantly checks for objects directly in front | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
