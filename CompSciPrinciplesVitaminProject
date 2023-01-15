import random
import math
from browser import timer

BED_WIDTH = 300
BED_HEIGHT = 30
BED_COLOR = Color.blue
BED_LEG_WIDTH = 5
BED_LEG_HEIGHT = 10
BED_LEG_COLOR = Color.yellow
GUY_RAD = 40
GUY_COLOR = Color.red
SUN_RAD = 50
SUN_OFFSET = 7
GAME_LENGTH = 20

bed = None
bed_leg_1 = None
bed_leg_2 = None
guy = None
vit_text_1 = None
vit_text_2 = None
vit_text_3 = None
instruct_text_1 = None
instruct_text_2 = None
sun = None
guy_eye_1 = None
guy_eye_2 = None
guy_smile = None

clicks = 0

start_text_1 = Text("CLICK THE MOUSE TO")
start_text_1.set_position(get_width()/2-start_text_1.get_width()/2,get_height()/2)
add(start_text_1)

start_text_2 = Text("BEGIN AND CONTINUE")
start_text_2.set_position(get_width()/2-start_text_2.get_width()/2,get_height()/2+start_text_1.get_height())
add(start_text_2)

def get_distance(x1,y1,x2,y2):
    return math.sqrt((x2-x1) ** 2 + (y2-y1) ** 2)
    
num_vitamins = 0
def create_game():
    #Array where falling Vitamin D balls are stored
    balls = []
    
    #Text for amount of Vitamin D collected; Displayed in top right
    score_text = Text("Vitamin D: " + str(num_vitamins))
    score_text.set_font("15pt Gill Sans")
    score_text.set_position(get_width() - score_text.get_width() - 15, score_text.get_height() + 10)
    add(score_text)
    
    #Creates character
    def create_character():
        global head
        head = Circle(GUY_RAD)
        head.set_color(GUY_COLOR)
        head.set_position(get_width()/2, get_height() - 2 * head.get_radius())
        add(head)
    
    #Creates a VItamin D ball at a random x value
    def create_ball():
        random_ball = Circle(10)
        random_ball.set_position(random.randint(10,get_width() - 10),0)
        random_ball.set_color(Color.YELLOW)
        add(random_ball)
        d_text = Text("D")
        d_text.set_font("10pt Arial")
        d_text.set_position(random_ball.get_x() - d_text.get_width()/2, random_ball.get_y() + d_text.get_height()/2)
        add(d_text)
        setattr(random_ball, "text", d_text)
        balls.append(random_ball)

    #Callback function to move character
    def move_head(x,y):
        head.set_position(x, head.get_y())
        
    #Callback function to make Vitamin D balls drop
    def move_balls_down():
        for ball in balls:
            ball.move(0,5)
            ball_text = getattr(ball, "text")
            ball_text.set_position(ball.get_x() - ball_text.get_width()/2, ball.get_y() + ball_text.get_height()/2)
    
    #Callback function that repeatedly checks if a Vitamin D ball comes in contact with the character
    def check_balls():
        global num_vitamins
        for ball in balls:
            if get_distance(ball.get_x(),ball.get_y(),head.get_x(),head.get_y()) < 50 + 10:
                remove(ball)
                remove(getattr(ball,"text"))
                balls.remove(ball)
                num_vitamins += 1
                score_text.set_text("Vitamin D: " + str(num_vitamins))
                
    def end_game():
        for ball in balls:
            remove(ball)
            remove(getattr(ball,"text"))
            balls.remove(ball)
        end_text = Text("You got so much Vitamin D!")
        end_text.set_position(get_width()/2 - end_text.get_width()/2 + 20, get_height()/2 + end_text.get_height()/2)
        end_text.set_font("20pt American Typewriter")
        add(end_text)
        remove(timer_text)
        handlers['mousemove'].remove(move_head)
        head.set_position(get_width()/2, get_height() - 2 * head.get_radius())
        
    def update_countdown():
        if(game_timer > 0):
            global game_timer
            game_timer -= 1
            timer_text.set_text(game_timer)
        else:
            timer.clear_interval(countdown_timer)
            timer.clear_interval(spawn_ball_timer)
            end_game()
            
            
    create_character()
    add_mouse_move_handler(move_head)
    spawn_ball_timer = timer.set_interval(create_ball, 1000)
    timer.set_interval(check_balls,5)
    timer.set_interval(move_balls_down,5)
    
    global game_timer
    game_timer = GAME_LENGTH
    timer_text = Text(game_timer)
    timer_text.set_font("15pt Times")
    timer_text.set_position(get_width()/2 - timer_text.get_width()/2, timer_text.get_height() + 10)
    add(timer_text)
    
            
    
    countdown_timer = timer.set_interval(update_countdown, 1000)
    
    



def add_bed():
    global bed
    bed = Rectangle(BED_WIDTH,BED_HEIGHT)
    bed.set_color(BED_COLOR)
    bed.set_position(get_width()/2-BED_WIDTH/2,get_height()-BED_HEIGHT-BED_LEG_HEIGHT)
    add(bed)

def add_legs():
    global bed_leg_1
    global bed_leg_2
    bed_leg_1 = Rectangle(BED_LEG_WIDTH, BED_LEG_HEIGHT)
    bed_leg_1.set_color(BED_LEG_COLOR)
    bed_leg_1.set_position(get_width()/2-BED_WIDTH/2,get_height()-BED_LEG_HEIGHT)
    add(bed_leg_1)
    bed_leg_2 = Rectangle(BED_LEG_WIDTH,BED_LEG_HEIGHT)
    bed_leg_2.set_color(BED_LEG_COLOR)
    bed_leg_2.set_position(get_width()/2+BED_WIDTH/2-BED_LEG_WIDTH,get_height()-BED_LEG_HEIGHT)
    add(bed_leg_2)
    
def add_guy():
    global guy
    guy = Circle(GUY_RAD)
    guy.set_color(GUY_COLOR)
    guy.set_position(get_width()/2,get_height()-BED_HEIGHT-GUY_RAD-BED_LEG_HEIGHT)
    add(guy)
    
    

def add_vd_text():
    global vit_text_1
    global vit_text_2
    global vit_text_3
    vit_text_1 = Text("I'm not getting enough Vitamin D")
    vit_text_2 = Text("It is good for me, and I can")
    vit_text_3 = Text ("get it from being in the sun.")
    vit_text_1.set_position(get_width()/2-vit_text_1.get_width()/2,get_height()/2)
    vit_text_2.set_position(get_width()/2-vit_text_2.get_width()/2,get_height()/2+vit_text_1.get_height())
    vit_text_3.set_position(get_width()/2-vit_text_3.get_width()/2,get_height()/2+vit_text_1.get_height()+vit_text_2.get_height())
    add(vit_text_1)
    add(vit_text_2)
    add(vit_text_3)

dude = None

def instruct_screen():
    global instruct_text_1
    global instruct_text_2
    global sun
    global dude
    sky = Rectangle(get_width(),get_height())
    sky.set_color(Color.blue)
    sky.set_position(0,0)
    add(sky)
    for i in range(7):
        ground = Circle(40)
        ground.set_position(i*get_width()/7+20,get_height())
        ground.set_color(Color.green)
        add(ground)
    dude = Circle(40)
    dude.set_color(Color.red)
    dude.set_position(get_width()/2,get_height()-40-BED_LEG_HEIGHT-BED_HEIGHT)
    add(dude)
    instruct_text_1 = Text("Collect the Vitamin D")
    instruct_text_2 = Text("<-Use your mouse to move->")
    instruct_text_1.set_position(get_width()/2-instruct_text_1.get_width()/2,get_height()/2)
    instruct_text_2.set_position(get_width()/2-instruct_text_2.get_width()/2,get_height()/2+instruct_text_1.get_height())
    add(instruct_text_1)
    add(instruct_text_2)
    sun = Circle(SUN_RAD)
    sun.set_color(Color.yellow)
    sun.set_position(SUN_RAD+SUN_OFFSET,SUN_RAD+SUN_OFFSET)
    add(sun)
    
    
background_one = None
    
def scene(x,y):
    if clicks == 0:
        global background_one
        background_one = Rectangle(get_width(),get_height())
        background_one.set_color(Color.orange)
        background_one.set_position(0,0)
        add(background_one)
        remove(start_text_1)
        remove(start_text_2)
        add_bed()
        add_legs()
        add_guy()
    elif clicks == 1:
    
        add_vd_text()
    elif clicks == 2:
        global background_one
        global vit_text_1
        global vit_text_2
        global vit_text_3
        global bed
        global bed_leg_2
        remove(vit_text_1)
        remove(vit_text_2)
        remove(vit_text_3)
        remove(bed)
        remove(bed_leg_1)
        remove(bed_leg_2)
        instruct_screen()
    elif clicks == 3:
        global instruct_text_1
        global instruct_text_2
        global guy
        global dude
        remove(dude)
        remove(instruct_text_1)
        remove(instruct_text_2)
        remove(guy)
        create_game()
    global clicks
    clicks = clicks +1


add_mouse_click_handler(scene)

