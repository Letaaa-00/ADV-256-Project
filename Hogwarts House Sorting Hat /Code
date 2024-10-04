import os, sys, io
import M5
from M5 import *
from hardware import *
import time
import random

# Initialize M5 board
M5.begin()

# Setup RGB (connected to Pin G2)
rgb2 = RGB(io=38, n=30, type="SK6812")

# Initialize circuit connection on Pin G6
circuit_pin = Pin(1, mode=Pin.IN, pull=Pin.PULL_UP)

# House colors (R, G, B)
house_colors = {
    1: (255, 0, 0),    # Gryffindor
    2: (0, 0, 255),    # Ravenclaw
    3: (255, 255, 0),  # Hufflepuff
    4: (0, 255, 0)     # Slytherin
}

# House names
house_names = {
    1: "Gryffindor",
    2: "Ravenclaw",
    3: "Hufflepuff",
    4: "Slytherin"
}

# Function to get the RGB color
def get_rgb_color(r, g, b):
    global rgb2
    rgb_color = (r << 16) | (g << 8) | b
    return rgb_color


# Flash lights function
def flash_lights():
    global rgb2
    i=0
    while (i<3):
        rgb2.fill_color(get_rgb_color(255, 0, 0))  # Red
        time.sleep(0.5)
        rgb2.fill_color(get_rgb_color(0, 0, 255))  # Blue
        time.sleep(0.5)
        rgb2.fill_color(get_rgb_color(255, 255, 0))  # Yellow
        time.sleep(0.5)
        rgb2.fill_color(get_rgb_color(0, 255, 0))  # Green
        time.sleep(0.5)
        i = i+1

# Function to select house and show color
def select_house():
    global rgb2
    house = random.randint(1, 4)
    color = house_colors[house]
    rgb2.fill_color(get_rgb_color(*color))
    print(house_names[house])  # Announce house name
    return house_names[house]


# Main loop (run only once when circuit connects)
while True:
    M5.update()

    # Detect if circuit is completed (Pin G6)
    if circuit_pin.value() == False:
    
        flash_lights()
        time.sleep(2)  # Pause before final selection
        selected_house = select_house()
        print(f"You are in {selected_house}!")
        break  # Exit after one cycle
    time.sleep(0.1)  # Small delay to prevent overload
