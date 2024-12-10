## Final Project Soft Robot Rescue
This project explores a soft robotic crawling tentacle designed for disaster search and rescue. 
With its ability to maneuver through tight spaces, 
it can navigate collapsed buildings and narrow gaps to locate trapped survivors, 
reaching areas inaccessible to traditional rescue equipment or larger robots.

Flexible, Precise, and Reliable.

Here is one cover image:
![Here is one image of my Hogwarts House Sorting Hat](cover.png)


### Part 1 - Introduction of my initial project idea
Here is my first ideation of sketch:  

This project uses a soft robot and reflective sensors for post-disaster search and rescue. The soft tentacles can pass through small spaces and the sensors can detect the presence of survivors. The robot can adjust its movements based on detected light and obstacles, while using green light to indicate the location of discovered survivors and provide simple medical support. The success of the rescue depends on the robot being able to safely reach the survivors and provide initial assistance.

![Here is one image of my sketch](sketch1.png)
![Here is one image of my sketch](sketch2.png)


### Part 2 - Process of making lanterns
I designed a soft robotic model inspired by octopus tentacles, focusing on its flexibility and crawling capability. The model was developed in Rhino and fabricated using silicone materials to ensure softness and durability. The crawling mechanism uses a pneumatic system to simulate the expansion and contraction of the tentacle. Reflective sensors were integrated into the design to detect light intensity and locate obstacles or survivors in disaster scenarios. Additionally, I incorporated a lightweight structure to house components such as the air pump, pressure regulator, and control module, ensuring the robot remains compact and maneuverable in tight spaces.

![Process of hidden M5 stack](sketch1.png)  
![Process of hidden M5 stack](assemble.png)  

Here is the list of all the separate hardware components used in Hogwarts House Sorting Hat
* Soft Robotic Model: The core of the project, designed to mimic the flexibility and movement of octopus tentacles. It uses pneumatic chambers to enable crawling through tight spaces. 
* Extention of ATOM: In order to additional input/output ports and enhancing connectivity options.  
* Reflective Sensor: Detects light intensity and helps locate survivors or obstacles by adjusting the robot's behavior based on the surrounding environment.
* Air Pump: Provides the pneumatic pressure required to inflate and deflate the robot's chambers, enabling movement.
* Air Pressure Regulator: Ensures consistent and controllable air pressure for precise motion control of the soft tentacle.
* Control Module (M5Stack): Manages sensor input and pneumatic control, running the program that coordinates the robot's movement and detection tasks.
* LED Indicator: Provides visual feedback, such as flashing or steady green light, to indicate detected survivors or operational status during rescue missions.

![Process of hidden M5 stack](assemble.png) 

### Part 4 - How my interactive prototype should behave
diagram that represents how my interactive prototype should behave  

![Code diagram](diagram.png)  

Allow me explain the inputs/outputs used in my code and how they affect the behavior of the lantern in Thonny.
* The code imports necessary modules, including the M5 library, time library, m5utils, and hardware module, enabling interaction with the M5Stack board and connected hardware components.
```Python
import os, sys, io
import M5
from M5 import 
import time
import m5utils
from hardware import 

```  

* An infinite while loop is used to continuously update the M5Stack's status (M5.update()), read sensor data, and control the RGB light strip's brightness. time.sleep_ms(50) adds a delay to control the loop’s execution frequency.
```Python
while True:
    M5.update()
    ...
    time.sleep_ms(50)
```  

* The set_brightness(scaled_val) function is called to apply the remapped brightness value to the RGB light strip.
* print(scaled_val) outputs the brightness value to the console for debugging and monitoring.
```Python
set_brightness(scaled_val)
print(scaled_val)

```

* RGB(io=38, n=30, type="SK6812") configures an RGB light strip connected to Pin 38, with 30 LEDs of type SK6812.
* ADC(Pin(7), atten=ADC.ATTN_11DB) sets up the ADC on Pin 7 with an attenuation setting of 11DB, increasing the ADC's input range.
```Python
rgb2 = RGB(io=38, n=30, type="SK6812")
adc = ADC(Pin(7), atten=ADC.ATTN_11DB)
```

* The set_brightness(brightness) function calculates the RGB color value for the light strip based on the brightness parameter.
* (brightness << 16) | (brightness << 8) | brightness converts the brightness level into an RGB color value representing white (R=G=B) with varying intensity.
* rgb2.fill_color(rgb_color) applies the computed color value to the entire RGB strip.

```Python
def set_brightness(brightness):
    rgb_color = (brightness << 16) | (brightness << 8) | brightness  # White with varying brightness
    rgb2.fill_color(rgb_color)

```
### Part 4 - How my interactive prototype should behave

Allow me explain the inputs/outputs used in my code and how they affect the behavior of in Digital Game.
* Imports the p5.js library for drawing and handling graphics (aliased as p5) and document from JavaScript, allowing access to HTML elements for interaction.
```Python
import js as p5
from js import document
```

* Initializes variables for different images used in the game, such as background_img, avatar_img, and several monster images.
```Python
# Load images
background_img = None
avatar_img = None
monster1_img = None
monster2_img = None
monster3_img = None
achieve_img = None
win_img = None

```

* Defines various game-related variables: monster_x for monster position, sensor_value for reading sensor input, brightness for screen brightness, game_state to track the game's status, and bg_x and bg_scale for handling background movement and scaling.

```Python
# Variables
monster_x = 500
sensor_value = 0
brightness = 255
monster_timer = 0
game_state = "play"  # states: play, game_over, win
monster_index = 0
monsters = []  # List to store the monster images
bg_x = 0  # For background movement
bg_scale = 1.5  # Scale factor for the background

```


* Loads all image assets needed for the game, such as the background, avatar, and monster images, storing them as global variables.

```Python
def preload():
    global background_img, avatar_img, monster1_img, monster2_img, monster3_img, achieve_img, win_img, monsters
    background_img = p5.loadImage("Background.png")
    avatar_img = p5.loadImage("Avatar.png")
    monster1_img = p5.loadImage("Monster1.png")
    monster2_img = p5.loadImage("Monster2.png")
    monster3_img = p5.loadImage("Monster3.png")
    achieve_img = p5.loadImage("achieve.png")
    win_img = p5.loadImage("win.png")
    monsters = [monster1_img, monster2_img, monster3_img]  # Load monsters into list

```

* Sets up the game by creating an 800x400 canvas and printing a message indicating that setup is complete.

```Python
def setup():
    p5.createCanvas(800, 400)  # Adjust canvas size
    print('Game setup complete')

```

* This function is called continuously to render the game frame-by-frame.

```Python
def draw():
    global monster_timer, sensor_value, brightness, game_state, monster_index, bg_x, monster_x
```


* Reads the value from a "data" HTML element (likely for a sensor) to adjust brightness, which then changes the background color accordingly.

```Python
    # Reading data from reflective sensor
    sensor_value = int(document.getElementById("data").innerText)
    brightness = int(sensor_value)
    
    # Adjust screen brightness
    p5.background(brightness)

```

* Moves the background to create a scrolling effect. When bg_x reaches a certain point, it resets to create a looped background.
```Python
       bg_x -= 10 * p5.deltaTime / 1000  # 10px per second movement
    if bg_x <= -background_img.width * bg_scale:  # Wrap background
        bg_x = 0
    
    # Scale and draw the background at its correct ratio
    p5.push()
    p5.scale(bg_scale)
    p5.image(background_img, bg_x / bg_scale, 200 / bg_scale)
    p5.image(background_img, (bg_x + background_img.width) / bg_scale, 200 / bg_scale)
    p5.pop()


```

* The game has three states: "play", "game_over", and "win". In "play" mode, the avatar and monsters are rendered, and game logic runs.
* Avatar Drawing: The avatar is displayed at a fixed position on the screen.
* Monster Logic: The monster moves horizontally. Every 10 seconds, it appears at a set position. Based on sensor_value, the game state changes to "game_over" or "win".
```Python
     if game_state == "play":
        # Avatar logic
        p5.image(avatar_img, 100, 240)
        
        # Monster logic (every 10 seconds)
        monster_timer += p5.deltaTime / 1000
        monster_x -= 20 * p5.deltaTime / 1000
        if monster_timer >= 10:
            p5.image(monster2_img, monster_x, p5.height - 350)  
        if monster_x <= 120 and sensor_value == 255:
            game_state = "game_over"
        if monster_x <= 120 and sensor_value == 12:
            game_state = "win"


```


* Displays different text and background colors based on whether the player has won or lost.
```Python
     elif game_state == "game_over":
        p5.background(0)  # Black screen
        p5.fill(255)  # White text
        p5.textSize(50)
        p5.textAlign(p5.CENTER, p5.CENTER)
        p5.text("You've been captured ", p5.width / 2, p5.height / 3)
        p5.text("by monster ", p5.width / 2, p5.height /2 )

    elif game_state == "win":
        p5.background(0)
        p5.fill(255)
        p5.textSize(50)
        p5.textAlign(p5.CENTER, p5.CENTER)
        p5.text("You survived from monster ", p5.width / 2, p5.height /2 )

```

* This function calculates the distance between the avatar and a fixed point to check if they collide, indicating the player reached the achievement.
```Python
 def avatar_touches_achieve():
    # Check if avatar touches achievement
    return p5.dist(200, 200, 600, p5.height - 150) < 50
