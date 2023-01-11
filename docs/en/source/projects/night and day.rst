###########
Night and Day
###########

Introduction
-------------
This game will be a game that you will use your attention and reflex. In this project, we will use a 0.96” 128x64 pixel I2C OLED display.

Project Details and Algorithm
------------------------------

How about playing the Night and Day game you played at school electronically? The game of night and day is a game in which we put our head on the table when our teacher says night, and raise our heads when our teacher says day. 

Since OLED screens can be used as an artificial light source, you can enlarge the characters on the screen using lenses and mirrors and reflect them on the desired plane. Systems that can reflect information, road and traffic information on smart glasses and automobile windows can be made using OLED screens. Light sensors are sensors that can measure the light levels of the environment they are in, also called photodiodes. The electrical conductivity of the sensor exposed to light changes. We can control the light sensor by coding and develop electronic systems that affect the amount of light.

First we will ask the player to press the button to start the game. Then we will make the OLED screen of PicoBricks display NIGHT and DAY randomly for 2 seconds each. The player should cover the LDR sensor with his hand within 2 seconds if the word written on the OLED screen is NIGHT, and if the word DAY is written on the OLED screen, the player should raise his hand over the LDR sensor. Each correct response of the player will earn 10 points. In case of wrong response, the game will be over and there will be a written statement on the screen stating the end of the game, a different tone will sound from the buzzer, and the score information will be displayed on the OLED screen. If the player gives a total of 10 correct responses and gets 100 points, the phrase ``Congratulation`` will be displayed on the OLED screen and the buzzer will play notes in different tones.


Wiring Diagram
--------------

.. figure:: ../_static/night-and-day.png      
    :align: center
    :width: 400
    :figclass: align-center
    



You can program and run Picobricks modules without any wiring. If you are going to use the modules by separating them from the board, then you should make the module connections with the Grove cables provided.

MicroPython Code of the Project
--------------------------------
.. code-block::

    from machine import Pin, I2C, Timer, ADC, PWM
    from picobricks import SSD1306_I2C
    import utime
    import urandom
    #define the libraries
    WIDTH = 128
    HEIGHT = 64
    #OLED Screen Settings
    sda=machine.Pin(4)
    scl=machine.Pin(5)
    #initialize digital pin 4 and 5 as an OUTPUT for OLED Communication
    i2c=machine.I2C(0,sda=sda, scl=scl, freq=1000000)
    oled = SSD1306_I2C(WIDTH, HEIGHT, i2c)
    buzzer = PWM(Pin(20))
    buzzer.freq(440)
    ldr=ADC(Pin(27))
    button=Pin(10,Pin.IN,Pin.PULL_DOWN)
    #define the input and output pins
    oled.text("NIGHT and DAY", 10, 0)
    oled.text("<GAME>", 40, 20)
    oled.text("Press the Button", 0, 40)
    oled.text("to START!", 40, 55)
    oled.show()
    #OLED Screen Texts Settings
    def changeWord():
    global nightorday
    oled.fill(0)
    oled.show()
    nightorday=round(urandom.uniform(0,1))
    #when data is '0', OLED texts NIGHT
    if nightorday==0:
        oled.text("---NIGHT---", 20, 30)
        oled.show()
    else:
        oled.text("---DAY---", 20, 30)
        oled.show()
    #waits for the button to be pressed to activate
        
    while button.value()==0:
    print("Press the Button")
    sleep(0.01)
    
    oled.fill(0)
    oled.show()
    start=1
    global score
    score=0
    while start==1:
    global gamerReaction
    global score
    changeWord()
    startTime=utime.ticks_ms()
    #when LDR's data greater than 2000, gamer reaction '0'
    while utime.ticks_diff(utime.ticks_ms(), startTime)<=2000:
        if ldr.read_u16()>20000:
            gamerReaction=0
        #when LDR's data lower than 2000, gamer reaction '1'
        else:
            gamerReaction=1
        sleep(0.01)
    #buzzer working
    buzzer.duty_u16(2000)
    sleep(0.05)
    buzzer.duty_u16(0)
    if gamerReaction==nightorday:
        score += 10
    #when score is 10, OLED says 'Game Over'
    else:
        oled.fill(0)
        oled.show()
        oled.text("Game Over", 0, 18, 1)
        oled.text("Your score " + str(score), 0,35)
        oled.text("Press RESET",0, 45)
        oled.text("To REPEAT",0,55)
        oled.show()
        buzzer.duty_u16(2000)
        sleep(0.05)
        buzzer.duty_u16(0)
        break;
    if score==100:
        #when score is 10, OLED says 'You Won'
        oled.fill(0)
        oled.show()
        oled.text("Congratulation", 10, 10)
        oled.text("Top Score: 100", 5, 35)
        oled.text("Press Reset", 20, 45)
        oled.text("To REPEAT", 25,55)
        oled.show()
        buzzer.duty_u16(2000)
        sleep(0.1)
        buzzer.duty_u16(0)
        sleep(0.1)
        buzzer.duty_u16(2000)
        sleep(0.1)
        buzzer.duty_u16(0)
        break;
            


.. tip::
  If you rename your code file to main.py, your code will run after every boot.
   
Arduino C Code of the Project
-------------------------------


.. code-block::

    #include <Wire.h>
    #include "ACROBOTIC_SSD1306.h"
    //define the library


    #define RANDOM_SEED_PIN     28
    int Gamer_Reaction=0;
    int Night_or_Day=0;
    int Score=0;
    int counter=0;

    double currentTime=0;
    double lastTime=0;
    double getLastTime(){
    return currentTime=millis()/1000.0-lastTime;
        }

    void _delay(float seconds){
    long endTime=millis()+seconds*1000;
    while (millis()<endTime) _loop();
        }

    void _loop(){
    }

    void loop(){
    _loop();
    }
    //define variable

    void setup() {
    // put your setup code here, to run once:
    pinMode(10,INPUT);
    pinMode(27, INPUT);
    pinMode(20,OUTPUT);
    randomSeed(RANDOM_SEED_PIN);
    Wire.begin();
    oled.init();
    oled.clearDisplay();
    //define the input and output pins

    oled.clearDisplay();
    oled.setTextXY(1,3);
    oled.putString("NIGHT and DAY");
    oled.setTextXY(2,7);
    oled.putString("GAME");
    oled.setTextXY(5,2);
    oled.putString("Press the BUTTON");
    oled.setTextXY(6,4);
    oled.putString("to START!");
    //write "NIGHT an DAY, GAME, Press the BUTTON, to START" on the x and y coordinates determined on the OLED screen

    Score=0;
    //define the score variable

    while(!(digitalRead(10)==1))  //until the button is pressed
        {
        _loop();
    }
    _delay(0.2);

    while(1){  //while loop
    if(counter==0){
      delay(500);
      Change_Word();
      lastTime=millis()/1000.0;
        }
    while(!(getLastTime()>2)){
      Serial.println(analogRead(27));
      if(analogRead(27)>200){
        Gamer_Reaction=0;

      }
      else{
        Gamer_Reaction=1;
      }
    }
    //determine the gamer reaction based on the value of the LDR sensor
    digitalWrite(20,HIGH);   //turn on the buzzer
    delay(250);  //wait
    digitalWrite(20,LOW);  //turn off the buzzer

    if(Night_or_Day==Gamer_Reaction){  //if the user's reaction and the Night_or_Day variable are the same
    Correct();
   
    }
    else{
    Wrong();
    }
    _loop();

    if(Score==100){
      oled.clearDisplay();
      oled.setTextXY(1,1);
      oled.putString("Congratulation");
      oled.setTextXY(3,1);
      oled.putString("Your Score");
      oled.setTextXY(3,13);
      String String_Score=String(Score);
      oled.putString(String_Score);
      oled.setTextXY(5,3);
      oled.putString("Press Reset");
      oled.setTextXY(6,3);
      oled.putString("To Repeat!");
      //write the "Congratulation, Your Score, press Reset, To Repeat!" and score variable on the x and y coordinates determined on the OLED screen
      for(int i=0;i<3;i++){
        digitalWrite(20,HIGH);
        delay(500);
        digitalWrite(20,LOW);
        delay(500);
     
    }
    //turn the buzzer on and off three times
    counter=1;

        }
        }
    }

    void Correct(){
    Score+=10;
    oled.clearDisplay();
    oled.setTextXY(3,4);
    oled.putString("10 Points");
    //increase the score by 10 when the gamer answers correctly
    }

    void Change_Word(){
  
    oled.clearDisplay();
    Night_or_Day=random(0,2);
    if(Night_or_Day==0){
    oled.setTextXY(3,6);
    oled.putString("NIGHT");

    }
    else{
    oled.setTextXY(3,7);
    oled.putString("DAY");
    }
 
    }
    //write "NIGHT" or "DAY" on random OLED screen

    void Wrong(){
    oled.clearDisplay();
    oled.setTextXY(1,3);
    oled.putString("Game Over");
    oled.setTextXY(3,1);
    oled.putString("Your Score");
    oled.setTextXY(1,13);
    String String_Score=String(Score);
    oled.putString(String_Score);
    oled.setTextXY(5,3);
    oled.putString("Pres Reset");
    oled.setTextXY(6,3);
    oled.putString("To Repeat");
    // write the score variable and the expressions is quotation marks to the coordinates determined on the OLED screen.

    digitalWrite(20,HIGH);  //turn on the buzzer
    delay(1000);   //wait
    digitalWrite(20,LOW); //turn off the buzzer
    counter=1;
    }

Coding the Project with MicroBlocks
------------------------------------
+----------------+
||night-and-day1||     
+----------------+

.. |night-and-day1| image:: _static/night-and-day1.png




.. note::
  To code with MicroBlocks, simply drag and drop the image above to the MicroBlocks Run tab.
  

    
