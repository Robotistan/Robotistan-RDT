###########
Action-Reaction
###########

Introduction
-------------
In the project, we will understand the pressing status by checking whether the button conducts current or not. If it is pressed, it will light the LED, if it is not pressed, we will turn off the LED.

   
As Newton explained in his laws of motion, a reaction occurs against every action. Electronic systems receive commands from users and perform their tasks. Usually a keypad, touch screen or a button is used for this job. Electronic devices respond verbally, in writing or visually to inform the user that their task is over and what is going on during the task. In addition to informing the user of these reactions, it can help to understand where the fault may be in a possible malfunction. 
In this project, you will learn how to receive and react to a command from the user in your projects by coding the button-LED module of Picobricks.

Project Details and Algorithm
------------------------------

There is 1 push button on Picobricks. They work like a ``switch``, they conduct current when pressed and do not conduct current when released.

Wiring Diagram
--------------

.. figure:: ../_static/action-reaction.png      
    :align: center
    :width: 500
    :figclass: align-center
    
.. figure:: ../_static/action-reaction-1.png      
    :align: center
    :width: 520
    :figclass: align-center


You can program and run Picobricks modules without any wiring. If you are going to use the modules by separating them from the board, then you should make the module connections with the Grove cables provided.

MicroPython Code of the Project
--------------------------------
.. code-block::

   from machine import Pin#to acces the hardware picobricks
   led = Pin(7,Pin.OUT)#initialize digital pin as an output for led
   push_button = Pin(10,Pin.IN,Pin.PULL_DOWN)#initialize digital pin 10 as an input
   while True:#while loop
    logic_state = push_button.value();#button on&off status
    if logic_state == True:#check the button and if it is on
        led.value(1)#turn on the led
    else:
        led.value(0)#turn off the led


.. tip::
  If you rename your code file to main.py, your code will run after every boot.
   
Arduino C Code of the Project
-------------------------------


.. code-block::

   void setup() {
  // put your setup code here, to run once:
  pinMode(7,OUTPUT);//initialize digital pin 7 as an output
  pinMode(10,INPUT);//initialize digital pin 10 as an input
  

   }
      void loop() {
  // put your main code here, to run repeatedly:
  if(digitalRead(10)==1){//check the button and if it is on
    digitalWrite(7,HIGH);//turn the LED on by making the voltage HIGH
  }
  else{
    digitalWrite(7,LOW);//turn the LED off by making the voltage LOW 
  }
  delay(10);//wait for half second

      }


Coding the Project with MicroBlocks
------------------------------------
+------------------+
||action-reaction3||     
+------------------+

.. |action-reaction3| image:: _static/action-reaction3.png


    

.. note::
To code with MicroBlocks, simply drag and drop the image above to the MicroBlocks Run tab.
  

    
