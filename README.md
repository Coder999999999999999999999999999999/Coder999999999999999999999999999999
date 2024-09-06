import pgzrun
import random

FONT_OPTION=(255, 255, 255)
WIDTH=800
HEIGHT=600

CENTER_X =WIDTH/2
CENTER_Y =HEIGHT/2

CENTER= (CENTER_X, CENTER_Y)

FINAL_LEVEL = 6
START_SPEED = 10

ITEMS = ["bag", "bottle", "chips", "battery"] #non recycle items

game_over=False
game_complete=False

current_level = 1

items=[]
animations=[]

def draw():
    global items, current_level, game_complete, game_over
    screen.clear()
    screen.blit("bground", (0, 0))
    if game_over:
        display_message("GAME OVER", "TRY AGAIN")
    elif game_complete:
        display_message("YOU WIN", "WELL DONE")
    else:
        for item in items:
            item.draw()

def display_message(heading, subheading):
    screen.draw.text(heading, fontsize=60, center=CENTER, colour="WHITE")
    screen.draw.text(subheading, fontsize=30, center=(CENTER_X, CENTER_Y+30), colour="WHITE")

def update():
    global items
    if len(items) == 0:
        items=make_items(current_level)

def make_items(number_of_extra_items):
    items_to_create= get_option_to_create(number_of_extra_items)
    new_items=create_items(items_to_create)
    animate_items(new_items)
    return new_items

def get_option_to_create(number_of_extra_items):
    items_to_create=["paper"]
    for i in range(0,number_of_extra_items):
        random_option=random.choice(ITEMS)
        items_to_create.append(random_option)
    return items_to_create

def create_items(items_to_create):
    new_items=[]
    for option in items_to_create:
        item = Actor(option+"img")
        new_items.append(item)
    return new_items


