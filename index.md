# Wandering Robot
Are you tired of your robot always falling off your desk as it drives on it's merry way. Well, I've developed a solution! My robot contains two IR sensors that detect when it has reached the edge of the desk or table. When it detected the edge, it will back up and turn, then resume moving forward.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Dana S | UH | Mechanical Engineering | Graduated

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone
Modifications to Project:
- Modifications to be done with kit parts: Add a start button, Add a bumper button, Add IR controller support
- Modifications to be done with Adafruit parts: Add back IR sensor to detect table edge, Add more powerful motors, Add separate battery pack for motors
- Challenges: Powering the motors and sensors via Arduino -> Had to change port that connects to motor driver, Broken motor driver -> Part arrived with ENB jumper cap broken, robot goes through 9V batteries very quickly

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Second Milestone
Wiring and Programming:
- I completed the wiring by referencing the provided instructions for the SunFounder kit [here](https://docs.sunfounder.com/projects/3in1-kit/en/latest/car_project/car_ir_obstacle.html). I programmed the Arduino by adapting the code provided by SunFounder [here](https://docs.sunfounder.com/projects/3in1-kit/en/latest/download_code.html). The file I modified can be found at the following file location: 3in1-kit-main > car_project > 5.obstacle_avoidance_module > 5.obstacle_avoidance_module.ino
- Modifications: I modified the wiring slightly to utilize a small breadboard. This allowed me to more easily power and ground the components. The original code that was provided was used for obstacles that are in front of the robot. My robot needed to move as long as there WAS an obstacle detected since it was looking for the table below it. I changed the code to invert all of the if statement conditions so it would move forward when an obstacle WAS detected and move backwards when an obstacle was not detected.
- Challenges: Due to the number of sensors and the motor driver needing to be powered, there was not enough space in the screw terminals to fit all of the necessary wires. I fixed this by incorporating the small breadboard. The IR sensors are very sensitive. I fixed this by continuously adjusting the potentiometers on the IR sensors for the different table conditions.
- Future Steps: I plan to further tune my robot for different table conditions and brainstorm additional features and modifications to improve my robot.

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# First Milestone
Building the Chassis:
- By following the provided instructions for the SunFounder kit [here](https://docs.sunfounder.com/projects/3in1-kit/en/latest/car_project/car_assemble.html), I built the chassis for my robot. I completed up to step 11 and modified step 12.
- Modified Step 12: Cut two strips of cardboard and tape one end to the backs of the IR sensors. Bend the cardboard to a 90 degree angle and tape the other end to the chassis such that the IR sensors are pointed back towards the table.
- Challenges: The procedure had you put the motors onto the chassis before putting on the stand-offs for the Arduino. This made it difficult to screw in the stand-offs. I would change the procedure to have the stand-offs put on first, then the motors.
- Future Steps: I plan to wire the robot and complete the programming by the next milestone.

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```Arduino

const int in1 = 5;
const int in2 = 6;
const int in3 = 9;
const int in4 = 10;

const int rightIR = 7;
const int leftIR = 8;

void setup() {
  Serial.begin(9600);

  //motor
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);

  //IR obstacle
  pinMode(leftIR, INPUT);
  pinMode(rightIR, INPUT);

}

void loop() {

  int left = digitalRead(leftIR);  // 0: Obstructed   1: Empty
  int right = digitalRead(rightIR);
  int speed = 150;

  // Serial.print("Left: ");
  // Serial.println(left);
  // Serial.print("Right: ");
  // Serial.println(right);

  if (left && !right) {
    backLeft(speed);
  } else if (!left && right) {
    backRight(speed);
  } else if (left && right) {
    moveBackward(speed);
  } else {
    moveForward(speed);
  }
}

void moveForward(int speed) {
  analogWrite(in1, 0);
  analogWrite(in2, speed);
  analogWrite(in3, speed);
  analogWrite(in4, 0);
  //Serial.println("forward");
}

void moveBackward(int speed) {
  analogWrite(in1, speed);
  analogWrite(in2, 0);
  analogWrite(in3, 0);
  analogWrite(in4, speed);
  //Serial.println("backward");
  //delay(100);
}

void backLeft(int speed) {
  analogWrite(in1, speed);
  analogWrite(in2, 0);
  analogWrite(in3, 0);
  analogWrite(in4, 0);
  //Serial.println("back left");
  //delay(100);
}

void backRight(int speed) {
  analogWrite(in1, 0);
  analogWrite(in2, 0);
  analogWrite(in3, 0);
  analogWrite(in4, speed);
  //Serial.println("back right");
  //delay(100);
}

```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
|:--:|:--:|:--:|:--:|

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
