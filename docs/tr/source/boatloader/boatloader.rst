###############
Bootloader
###############

BOOTSEL
--------

Pico’s BOOTSEL mode lives in read-only memory inside the RP2040 chip, and can’t be overwritten accidentally. No matter what, if you hold down the BOOTSEL button when you plug in your Pico, it will appear as a drive onto which you can drag a new UF2 file. There is no way to brick the board through software. However, there are some circumstances where you might want to make sure your Flash memory is empty. You can do this by dragging and dropping a special UF2 binary onto your Pico when it is in mass storage mode.


* Download the MicroPython ``UF2 file`` from the Raspberry Pi website
* Hold down the ``BOOTSEL`` button on your Pico and plug it into your computer's USB port.
* Open Explorer, and open the ``RPI-RP2 directory`` like you would any other hard drive
* Drag and drop the ``UF2 file`` into the ``RPI-RP2 directory``


Reset Flash Memory
-------------------

The Raspberry Pi Pico is a fantastic piece of technology, but it does have one flaw: ``there is no reset button``. How important is this omission? Sometimes our code can go away, or we need to flash new firmware to our Pico.

When this happens we have to unplug the Pico and plug it back in again in order to reset it. If we pull out the micro USB lead, a mechanical connection which is rated for a finite number of insertions, too many times, we could wear it out. If we have the Pico connected to a powered USB hub with on / off buttons, we can press the button on that, but what if we don’t.

.. tip::
  With very little equipment, and zero code we can build a simple button to reset our Pico ready for the next project.
  
Reset Button Project
---------------------

+---------------+---------------+
| What You Need For This        | 
+===============+===============+
| A Raspberry Pi Pico           | 
+---------------+---------------+
| 2 x Male to Male Jumper Wires | 
+---------------+---------------+
| Breadboard                    | 
+---------------+---------------+
| Pushbutton                    | 
+---------------+---------------+

1) Place the Raspberry Pi Pico into the breadboard so that the micro USB port hangs over ``the end of the breadboard.``

.. figure:: ../_static/pico1.png
    :align: center
    :width: 520
    :figclass: align-center

    
2) Insert a ``push button`` as you see in the image

.. figure:: ../_static/pico2.png
    :align: center
    :width: 520
    :figclass: align-center

    
3) Connect one of the jumper wires to the GND pin and the right leg of the button, and connect the other to the RUN pin and the left leg of the button.

.. figure:: ../_static/pico3.png
    :align: center
    :width: 520
    :figclass: align-center

    
.. note::
  Our reset button is ready to use.
  
.. tip::
  You can also check `Raspberry Pi Website <https://www.raspberrypi.com/documentation/microcontrollers/raspberry-pi-pico.html#resetting-flash-memory>`_ for more information.
   

