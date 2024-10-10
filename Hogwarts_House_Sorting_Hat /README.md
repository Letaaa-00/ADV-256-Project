## Project 1 Hogwarts House Sorting Hat Describtion  
I designed my first project based on the impressive Sorting Hat from the Harry Potter movies. 
People wear it, and it flashes the colors representing the different schools, and then randomly assigns you to one.
House of Gryffindor in red, Ravenclaw in blue,Hufflepuff in yellow and Slytherin in green.  

Here is one image of my Hogwarts House Sorting Hat:
![Here is one image of my Hogwarts House Sorting Hat](Hat.png)


### Part 1 - Introduction of my initial project idea
Here is my first two ideation of sketchs:  

This project involves creating an interactive Harry Potter Sorting Hat using an M5Stack development board, RGB LEDs, and copper plates as sensors. When the circuit is completed (by touching two copper plates), the hat begins a sequence of flashing colors representing Hogwarts houses: Gryffindor (red), Ravenclaw (blue), Hufflepuff (yellow), and Slytherin (green). After the flashing, a random house is selected, and the corresponding color lights up. The program announces the house, completing the magical sorting experience.  

![Here is one image of my Hogwarts House Sorting Hat](Ideation.png)


### Part 2 - Test Copper
After connecting to the M5, I first tested to see if the code for my copper's connection worked.
![How it build in UIFLOW](UIFLOW.png)
```Python
import os, sys, io
import M5
from M5 import *
from hardware import *



pin8 = None


def setup():
  global pin8

  M5.begin()
  pin8 = Pin(8, mode=Pin.IN, pull=Pin.PULL_DOWN)


def loop():
  global pin8
  M5.update()
  if pin8.value():
    print('Connect Successful')


if __name__ == '__main__':
  try:
    setup()
    while True:
      loop()
  except (Exception, KeyboardInterrupt) as e:
    try:
      from utility import print_error_msg
      print_error_msg(e)
    except ImportError:
      print("please update to latest firmware")
```
![During test with copper](Copper.png)

### Part 3 - Figure out where my copper should place
Then I had to decide where I should put the copper, but because the hat is so soft,
the first and second places I looked were both a clip on the brim, and after putting the hat back on, 
there was compression, and the two copper overlapped. Unfortunately, because the hat is soft, the chances of success are not high.  
![During test with copper](position1.png)  

Then I had to decide where to put the copper. But because the hat was so soft, the first and second places I tried were both a clip on the brim, and after putting the hat back on, the two copper overlapped due to the pressure. Unfortunately, because the hat was so soft, the chances of success were not high.
I then decided to sew the copper to the brim of the hat, then sew a piece of fabric on, and then sew a copper on the inside. When the person puts on the hat and their head pushes up, the two copper can meet and connect the circuit.  
![During test with copper](Sew.JPG)  

Here is the list of all the separate hardware components used in Hogwarts House Sorting Hat
* ATOM Lite: The core of the project, it controls the input/output and runs the program. It reads the circuit's state and controls the LEDs.  
* Extention of ATOM: In order to additional input/output ports and enhancing connectivity options.  
* RGB light stripe:  Represent the Hogwarts houses with different colors (red, blue, yellow, and green). They are connected to G2 and provide visual feedback during the sorting process.  
* Copper with wire: Act as sensors. When they touch, they close the circuit, triggering the sorting sequence.  

### Part 4 - How my interactive prototype should behave
diagram that represents how my interactive prototype should behave
![Code diagram](Diagram.png)  

And here is my code link:
[Hogwarts House Sorting Hat Code](main.py)

### Part 5 - Some video records for sort into different house
Here is a video I recorded using the branch hat to divide into the different Hogwarts houses.
Gryffindor
![Hogwarts House Sorting Hat video Gryffindor](Gryf.MOV)
Ravenclaw
![Hogwarts House Sorting Hat video Ravenclaw](Raven.mov)
Hufflepuff
![Hogwarts House Sorting Hat video Hufflepuff](Huff.MOV)
Slytherin
![Hogwarts House Sorting Hat video Slytherin](Sly.MOV)





