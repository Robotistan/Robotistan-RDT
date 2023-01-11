###########
Thermometer
###########

Introduction
-------------
In this project, you will prepare a thermometer with Picobricks that will display the ambient temperature on the OLED screen.

Sensors are the sense organs of electronic systems. We use our skin to feel, our eyes to see, our ears to hear, our tongue to taste, and our nose to smell. There are already many sense organs (sensors) in the picobrix. Also, new ones can be added. You can interact with the environment using humidity, temperature, light and many more sensors. Picobricks can measure the ambient temperature without the need for any other environmental component. Ambient temperature is used in greenhouses, incubators, in environments used for the transport of drugs, briefly in situations where the temperature change must be constantly monitored. If you are going to do an operation on temperature change in your projects, you should know how to measure the ambient temperature.

Project Details and Algorithm
------------------------------

Picobricks has a DHT11 module. This module can sense the temperature and humidity in the environment and send data to the microcontroller. In this project, we will write the necessary codes to print the temperature values measured by the DHT11 temperature and humidity sensor on the OLED screen.

Wiring Diagram
--------------

.. figure:: ../_static/thermometer.png
    :align: center
    :width: 500
    :figclass: align-center
    
.. figure:: ../_static/thermometer1.png
    :align: center
    :width: 520
    :figclass: align-center


You can program and run Picobricks modules without any wiring. If you are going to use the modules by separating them from the board, then you should make the module connections with the Grove cables provided.

MicroPython Code of the Project
--------------------------------
.. code-block::

  from machine import Pin,I2C,ADC #to acces the hardware picobricks
  from picobricks import SSD1306_I2C, DHT11 #oled library
  import utime #time library
  #to acces the hardware picobricks
  WIDTH=128
  HEIGHT=64
  #define the weight and height picobricks

  sda=machine.Pin(4)
  scl=machine.Pin(5)
  #we define sda and scl pins for inter-path communication
  i2c=machine.I2C(0, sda=sda, scl=scl, freq=2000000)#determine the frequency values
  oled=SSD1306_I2C(WIDTH, HEIGHT, i2c)
  pico_temp=DHT11(Pin(11))
  current_time=utime.time()
  while True:
    if(utime.time() - current_time > 2):
        current_time = utime.time()
        pico_temp.measure()
        oled.fill(0)#clear OLED
        oled.show()
        temperature=pico_temp.temperature
        humidity=pico_temp.humidity
        oled.text("Temperature: ",15,10)#print "Temperature: " on the OLED at x=15 y=10
        oled.text(str(int(temperature)),55,25)
        oled.text("Humidty: ", 30,40)
        oled.text(str(int(humidity)),55,55)
        oled.show()#show on OLED
        utime.sleep(0.5)#wait for a half second
   


.. tip::
  If you rename your code file to main.py, your code will run after every boot.
   
Arduino C Code of the Project
-------------------------------


.. code-block::

   #include <Wire.h>
   #include <DHT.h>
   #include "ACROBOTIC_SSD1306.h"
   #define DHTPIN 11
   #define DHTTYPE DHT11
   //define the library

   DHT dht(DHTPIN, DHTTYPE);
   float temperature;
   //define the temperature veriable

   void setup() {
   //define dht sensor and Oled screen
   Serial.begin(115200);
   dht.begin();
   Wire.begin();  
   oled.init();                      
   oled.clearDisplay(); 
      }

   void loop() {
   temperature = dht.readTemperature();
   Serial.print("Temp: ");
   Serial.println(temperature);
   oled.setTextXY(3,1);              
   oled.putString("Temperature: ");
   //print "Temperature: " on the OLED at x=3 y=1
   oled.setTextXY(4,3);              
   oled.putString(String(temperature));
   //print the value from the temperature sensor to the oled screen at x=4 y=3
   Serial.println(temperature);
   delay(100);
      }


Coding the Project with MicroBlocks
------------------------------------
+--------------+
||thermometer2||     
+--------------+

.. |thermometer2| image:: _static/thermometer2.png



.. note::
  To code with MicroBlocks, simply drag and drop the image above to the MicroBlocks Run tab.
  

    
