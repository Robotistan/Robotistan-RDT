#############################################
Thonny (MicroPython) IDE for Beginners
#############################################


.. figure:: ../_static/man.jpg
    :align: center
    :width: 720
    :figclass: align-center
    
    
Thonny IDE Setup
----------------

At the heart of Picobricks is the Raspberry Pi Pico. The Thonny Raspberry Pi is a great choice for coding Pico and therefore Picobricks.
Visit `Thonny Website <https://thonny.org/>`_ Select the version suitable for your system and download it to your computer. Then perform the installation. You can also install the Thonny IDE, using the command “ $ pip install thonny “

.. code-block::

  $ pip install thonny

.. figure:: ../_static/thonny.png
    :align: center
    :width: 420
    :figclass: align-center
    
Thonny IDE Interface
-----------------------


.. figure:: ../_static/thonny1.png
    :align: center
    :width: 920
    :figclass: align-center
    
    
A: Opens an empty script file.
B: Allows you to open an existing code file.
C: Allows you to save changes to the code file you are working on.
D: Runs the code you wrote in the interpreter environment you specify.
E: Allows you to check for errors in your code.
F: Allows you to run lines of code in order to debug.
G: Lets you navigate through the commands in the line of code while debugging.
H: Lets you exit debug.
I: Allows you to switch from debug mode to run mode.
J: Makes the code stop executing.

Upload MicroPython Firmware to Raspberry Pi Pico
-------------------------------------------------

In order for Raspberry Pi Pico to understand the MicroPython code we will write, we must install a special operating system for it. We call this firmware. Open the Thonny editor and click Select interpreter from the Run menu.

.. figure:: ../_static/thonny3.png
    :align: center
    :width: 720
    :figclass: align-center
    
Select the Raspberry Pi Pico from the drop-down list shown in area 1. Leave the 2nd area as in the image, click on the 3rd area.

.. figure:: ../_static/thonny2.png
    :align: center
    :width: 520
    :figclass: align-center
    
Connect Pico to your computer's USB port with a cable while ``holding down the white bootsel button`` on it.

.. figure:: ../_static/arduino3.png
    :align: center
    :width: 520
    :figclass: align-center
    
After the Install button is activated, you can release the button. Press the ``Install button`` and wait for the firmware to load.

.. figure:: ../_static/thonny4.png
    :align: center
    :width: 520
    :figclass: align-center
    
After the installation is complete, click the Close button to complete the installation.


Installing and Running Code on Raspberry Pi Pico
-------------------------------------------------

Plug the Pico's cable directly into the computer's USB port. You don't need to hold down the Bootsel button. Select the ``“Select interpreter”`` option from the Run menu in Thonny. Make sure Raspberry Pi Pico is selected in section 1. Click the OK button to close the window.

.. figure:: ../_static/thonny5.png
    :align: center
    :width: 520
    :figclass: align-center

Activate the Files option from the View menu. A long file explorer tab will be placed on the left side of the screen. If you see Raspberry Pi Pico in section 1, it means that it is connected to Thonny Pico without any problems, you are ready to write, save and run your code. File explorer area that shows the working directory on your computer.

The MicroPython code you wrote in Thonny consist of libraries arranged for Raspberry Pi Pico and similar micro control cards and are called MicroPython. The syntax and almost all libraries work the same as MicroPython.
The ``"hello world"`` application of the software world is the ``"blink"`` application to physical programming. Write down the code shown in field 1. Click the save button in area 2. Thonny will ask you in the window in area 3 whether you want to save your code in the working directory on your computer or in Pico's onboard memory. If you choose your computer, the resulting file will appear in field 4, and if you choose Pico, the resulting file will appear in field

.. figure:: ../_static/thonny6.png
    :align: center
    :width: 520
    :figclass: align-center
    
Select Raspberry Pi Pico from the Save in window, type ``“blink.py”``  in the File Name field and click the OK button.After seeing the ``"blink.py"`` file in Pico's file explorer, click the F5 key on the keyboard or the green Run button on the toolbar, and the code file will be run by Pico. If you see the internal LED on the Pico blinking at 1 second intervals, you have successfully written and run your first code. Congratulations :)

.. note::
   If you want the code you have written to run as soon as Pico is opened without giving a run command, you should save your code in Pico's main directory with the name ``"main.py".``

