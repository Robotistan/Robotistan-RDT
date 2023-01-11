###########
Two Axis Robot Arm
###########

Introduction
-------------
In this project you will learn about robot arm with Picobricks.

Project Details and Algorithm
------------------------------


Robot arms have replaced human power in the industrial field. In factories, robotic arms undertake the tasks of carrying and turning loads of weights and sizes that cannot be carried by a human. Being able to be positioned with a precision of one thousandth of a millimeter is above the sensitivity that a human hand can exhibit. When you watch the production videos of automobile factories, you will see how vital the robot arms are. The reason why they are called robots is that they can be programmed to do the same work with endless repetitions. The reason why it is called an arm is because it has an articulated structure like our arms. How many different directions a robot arm has the ability to rotate and move is expressed as axes. Robot arms are also used for carving and shaping aluminum and various metals. These devices, which are referred to as 7-axis CNC Routers, can shape metals like a sculptor shapes mud. According to the purpose of use in robot arms, stepper motor and servo motors, which are a kind of electric motor, are used. PicoBricks allows you to make projects with servo motors.

In preparation for the installation, we will first write and upload the codes to set the servo motors to 0 degrees. When an object is placed on the LDR sensor, the robot arm will bend down and close its open gripper. After the gripper is closed, the robot arm will rise again. As a result of each movement of the robot arm, a short beep will be heard from the buzzer. The RGB LED will glow red when an object is placed on the LDR sensor. When the object is held by the robot arm and lifted into the air, the RGB LED will turn green. Servo motor movements are very fast. In order to slow down the movement, we will code the servo motors with a total of 90 degrees of movement, 2 degrees each at 30 millisecond intervals. We’re not going to do this for the gripper to close.

Wiring Diagram
--------------

.. figure:: ../_static/two-axis-robot-arm.png      
    :align: center
    :width: 400
    :figclass: align-center
    


You can program and run Picobricks modules without any wiring. If you are going to use the modules by separating them from the board, then you should make the module connections with the Grove cables provided.

MicroPython Code of the Project
--------------------------------
.. code-block::

    from machine import Pin, PWM, ADC
    from utime import sleep
    from picobricks import WS2812
    #define libraries

    ws = WS2812(6, brightness=0.3)
    ldr=ADC(27)
    buzzer=PWM(Pin(20, Pin.OUT))
    servo1=PWM(Pin(21))
    servo2=PWM(Pin(22))
    #define LDR, buzzer and servo motors pins

    servo1.freq(50)
    servo2.freq(50)
    buzzer.freq(440)
    #define frequencies of servo motors and buzzer

    RED = (255, 0, 0)
    GREEN = (0, 255, 0)
    BLACK = (0, 0, 0) # RGB color settings
    angleupdown=4770
    angleupdown2=8200

    def up():
    global angleupdown
    for i in range (45):
        angleupdown +=76 
        servo2.duty_u16(angleupdown)
        sleep(0.03)
    buzzer.duty_u16(2000)
    sleep(0.1)
    buzzer.duty_u16(0)
    # servo2 goes up at specified intervals
    def down():
    global angleupdown
    for i in range (45):
        angleupdown -=76
        servo2.duty_u16(angleupdown)
        sleep(0.03)
    buzzer.duty_u16(2000)
    sleep(0.1)
    buzzer.duty_u16(0)
    # servo2 goes down at specified intervals

    def open():
    global angleupdown2
    for i in range (45):
        angleupdown2 +=500
        servo1.duty_u16(angleupdown2)
        sleep(0.03)
    buzzer.duty_u16(2000)
    sleep(0.1)
    buzzer.duty_u16(0)
    # servo1 works for opening the clamps
    def close():
    global angleupdown2
    for i in range (45):
        angleupdown2 -=500
        servo1.duty_u16(angleupdown2)
        sleep(0.03)
    buzzer.duty_u16(2000)
    sleep(0.1)
    buzzer.duty_u16(0)
    # servo1 works for closing the clamps
    open()
    servo2.duty_u16(angleupdown)
    ws.pixels_fill(BLACK)
    ws.pixels_show()
    while True:
    if ldr.read_u16()>20000:
        ws.pixels_fill(RED)
        ws.pixels_show()
        sleep(1)
        buzzer.duty_u16(2000)
        sleep(1)
        buzzer.duty_u16(0)
        open()
        sleep(0.5)
        down()
        sleep(0.5)
        close()
        sleep(0.5)
        up()
        ws.pixels_fill(GREEN)
        ws.pixels_show()
        sleep(0.5)
        # According to the data received from LDR, RGB LED lights red and green and servo motors move
            


.. tip::
  If you rename your code file to main.py, your code will run after every boot.
   
Arduino C Code of the Project
-------------------------------


.. code-block::

    #include <Adafruit_NeoPixel.h>
    #ifdef __AVR__
    #include <avr/power.h>
    #endif
    #define PIN        6
    #define NUMPIXELS 1
    Adafruit_NeoPixel pixels(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);
    #define DELAYVAL 500
    // define required libraries
    #include <Servo.h>
    Servo myservo1;
    Servo myservo2;

    int angleupdown;

    void setup() {

    pinMode(20,OUTPUT);
    pinMode(27,INPUT);
    // define input and output pins

    pixels.begin();
    pixels.clear();

    myservo1.attach(21);
    myservo2.attach(22); // define servo motor pins
    Open();
    angleupdown=180;
    myservo2.write(angleupdown);
  
        }

    void loop() {
    if(analogRead(27)>150){

    pixels.setPixelColor(0, pixels.Color(255, 0, 0));
    pixels.show();
    delay(1000);
    tone(20,700);
    delay(1000);
    noTone(20);

    Open();
    delay(500);
    Down();
    delay(500);
    Close();
    delay(500);
    Up();
    pixels.setPixelColor(0, pixels.Color(0, 255, 0));
    pixels.show();
    delay(10000);
    pixels.setPixelColor(0, pixels.Color(0, 0, 0));
    pixels.show();
    Open();
    angleupdown=180;
    myservo2.write(angleupdown);
    // If the LDR data is greater than the specified limit, the buzzer will sound, the RGB will turn red and servo motors will work
    // The RGB will turn green when the movement is complete
    
        }
    }

    void Open(){
    myservo1.write(180);
        }

    void Close(){
    myservo1.write(30);
        }

    void Up(){

    for (int i=0;i<45;i++){

    angleupdown = angleupdown+2;
    myservo2.write(angleupdown);
    delay(30);
    }
    }

    void Down(){

    for (int i=0;i<45;i++){

    angleupdown = angleupdown-2;
    myservo2.write(angleupdown);
    delay(30);
        }
        }

Coding the Project with MicroBlocks
------------------------------------
+---------------------+
||two-axis-robot-arm2||     
+---------------------+

.. |two-axis-robot-arm2| image:: _static/two-axis-robot-arm2.png



.. note::
  To code with MicroBlocks, simply drag and drop the image above to the MicroBlocks Run tab.
  

    
