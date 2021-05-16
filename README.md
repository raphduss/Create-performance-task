import pygame #Pygame is a module used for writing video games

#define all the colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
BLUE = (0, 0, 255)
GREEN = (39, 174, 96)
RED = (255, 0, 0)
PURPLE = (165, 105, 189)
GREY = (112, 123, 124)
BROWN = (214, 137, 16)
ORANGE = (255, 166, 0)
YELLOW = (255, 237, 17)
BRIGHTYELLOW = (255, 251, 20)
LIGHTBLUE = (133, 193, 233)
TURQUOISE = (22, 160, 133)
DARKGREEN = (20, 90, 50)
DARKRED = (139,0,0)
DARKPURPLE = (36, 0, 84)

import random #I will be using random to generate random colors

#Sets a range of colors that will be randomized whenever random_color is called
def random_color():
    levels = range(32,256,32) 
    return tuple(random.choice(levels) for _ in range(3)) 

class Wall(pygame.sprite.Sprite):#creates a wall class
 
    def __init__(self, x, y, width, height, color):#contructing the wall giving it a x and value, witch, height and color.
 
        super().__init__()#Call the parent's constructor
 
        self.image = pygame.Surface([width, height])#Gives the walls a width and height
        self.image.fill(color)#This allows the walls to have color which can be specified in the room classes
        
        #this makes the top left corner the passed-in location
        self.rect = self.image.get_rect()
        self.rect.x = x
        self.rect.y = y

class Player(pygame.sprite.Sprite):#creates a player class
 
    #speed of player (later modified using the movement keys)
    change_x = 0
    change_y = 0
 
    def __init__(self, x, y):#define the contructer function of the player sprite
 
        super().__init__()#Calls the parent's constructor
 
        self.image = pygame.Surface([5, 15])#sets the size of the player in pixels (width=15 , height=15)
        self.image.fill(random_color())#sets the color of the player to random
        
        #this makes the top left corner the passed-in location
        self.rect = self.image.get_rect()
        self.rect.y = y
        self.rect.x = x
 
    def changespeed(self, x, y):#define the speed of the player
        #changes the speed of player sprite depending on what key the player hits.
        self.change_x += x
        self.change_y += y
 
    def move(self, walls):#define a new position for the player
 
        self.rect.x += self.change_x#Move left/right
 
        block_hit_list = pygame.sprite.spritecollide(self, walls, False)#Did the player hit wall going left or right
        for block in block_hit_list:#for each wall that player hit
            if self.change_x > 0:#if player is moving right and collides with a wall
                self.rect.right = block.rect.left#Right x-coordinate of the player is set at the same x-coordinate as the left side of the wall
            else:
                self.rect.left = block.rect.right#Left x-coordinate of the player is set at the same x-coordinate as the right side of the wall
 
        self.rect.y += self.change_y#Move up/down
 
        block_hit_list = pygame.sprite.spritecollide(self, walls, False)#Did the player hit wall going up or down
        for block in block_hit_list:#for each wall that player hit
            if self.change_y > 0:#if player is moving down and collides with a wall
                self.rect.bottom = block.rect.top#Bottom y-coordinate of the player is set at the same y-coordinate as the top side of the wall
            else:
                self.rect.top = block.rect.bottom#Top y-coordinate of the player is set at the same y-coordinate as the bottom side of the wall
   
class Room(object):#creates a base room class
 
    wall_list = None#empty list of walls under the room class 
 
    def __init__(self):#contructer function creates the wall lists
        self.wall_list = pygame.sprite.Group()

class Room1(Room):#creates the walls found in room1

    #calls parent contructer
    def __init__(self):
        super().__init__()

        #list of walls([x, y, width, height])
        walls = [[0, 0, 800, 20, TURQUOISE],
                 [0, 580, 800, 20, TURQUOISE],
                 
                 [0, 0, 20, 250, TURQUOISE],
                 [0, 350, 20, 190, TURQUOISE],
                 [0, 580, 20, 20, TURQUOISE],
                 
                 [780, 0, 20, 20, TURQUOISE],
                 [780, 60, 20, 190, TURQUOISE],
                 [780, 350, 20, 250, TURQUOISE],

                 [390, 80, 20, 20, BLUE],
                 [390, 120, 20, 360, BLUE],
                 [390, 500, 20, 20, BLUE],
                 
                 [190, 100, 20, 400, BLUE],
                 [590, 100, 20, 400, BLUE],
                 
                 [235, 290, 130, 20, LIGHTBLUE],
                 [435, 290, 130, 20, LIGHTBLUE],
                 
                 [290, 60, 20, 200, GREY],
                 [490, 60, 20, 200, GREY],
                 [290, 340, 20, 200, GREY],
                 [490, 340, 20, 200, GREY],
                 
                 [20, 60, 100, 20, PURPLE],
                 [120, 60, 20, 115, PURPLE],
                 [120, 60, 160, 20, PURPLE],
                 
                 [20, 520, 100, 20, PURPLE],
                 [120, 425, 20, 115, PURPLE],
                 [120, 520, 160, 20, PURPLE],
                 
                 [680, 60, 100, 20, PURPLE],
                 [660, 60, 20, 115, PURPLE],
                 [520, 60, 140, 20, PURPLE],
                 
                 [680, 520, 100, 20, PURPLE],
                 [660, 425, 20, 115, PURPLE],
                 [520, 520, 140, 20, PURPLE],
                 
                 [420, 500, 60, 20, PURPLE],
                 [420, 80, 60, 20, PURPLE],
                 [320, 500, 60, 20, PURPLE],
                 [320, 80, 60, 20, PURPLE],
                ]

        for item in walls:#loops through each wall
            wall = Wall(item[0], item[1], item[2], item[3], item[4])#creates the wall
            self.wall_list.add(wall)#adds the wall to wall_list created in the base class
        
class Room2(Room):#creates room2 and the walls found in it

    #calls parent contructer
    def __init__(self):
        super().__init__()
 
         #list of walls([x, y, width, height])
        walls = [[0, 0, 20, 250, BROWN],
                 [0, 350, 20, 250, BROWN],
                 [780, 0, 20, 250, BROWN],
                 [780, 350, 20, 250, BROWN],
                 [20, 0, 760, 20, BROWN],
                 [20, 580, 760, 20, BROWN],
                 [190, 50, 20, 500, GREEN],
                 [590, 50, 20, 500, GREEN],
                 [240, 290, 320, 20, YELLOW],
                 [20, 115, 70, 20, YELLOW],
                 [20, 450, 70, 20, YELLOW],
                 [120, 60, 20, 480, YELLOW],
                 [710, 115, 70, 20, YELLOW],
                 [710, 450, 70, 20, YELLOW],
                 [660, 60, 20, 480, YELLOW],
                 
                 [290, 20, 20, 230, DARKGREEN],
                 [490, 20, 20, 230, DARKGREEN],
                 [290, 350, 20, 230, DARKGREEN],
                 [490, 350, 20, 230, DARKGREEN],
                 
                ]
 
        for item in walls:#loops through each wall
            wall = Wall(item[0], item[1], item[2], item[3], item[4])#creates the wall
            self.wall_list.add(wall)#adds the wall to wall_list created in the base class
        
class Room3(Room):#creates room3 with the walls found in it

    #calls parent contructer
    def __init__(self):
        super().__init__()
 
        walls = [[0, 0, 20, 250, BRIGHTYELLOW],
                 [0, 350, 20, 250, BRIGHTYELLOW],
                 [780, 0, 20, 250, BRIGHTYELLOW],
                 [780, 350, 20, 250, BRIGHTYELLOW],
                 [20, 0, 760, 20, BRIGHTYELLOW],
                 [20, 580, 760, 20, BRIGHTYELLOW],
                ]
 
        for item in walls:#loops through each wall
            wall = Wall(item[0], item[1], item[2], item[3], item[4])#creates the wall
            self.wall_list.add(wall)#adds the wall to the wall list created in the base class
 
    
        for x in range(40, 750, 75):#sets a x-range for mulitple walls(x-range = 50 -> 750)(space between walls = 75)
            for y in range(50, 550, 75):#sets a y-range for mulitple walls(y-range = 50 -> 550)(space between walls = 75)
                wall = Wall(x, y, 50, 50, ORANGE)#creates the walls (width = 50, height = 50, color = ORANGE)
                self.wall_list.add(wall)#adds the wall to the wall_list
 
        for x in range(115, 700, 75):#sets a x-range for mulitple walls(x-range = 115 -> 700)(space between walls = 75)
            for y in range(125, 500, 75):#sets a y-range for mulitple walls(y-range = 125 -> 500)(space between walls = 75)
                wall = Wall(x, y, 50, 50, RED)#creates the walls (width = 50, height = 50, color = RED)
                self.wall_list.add(wall)#adds the wall to the wall_list

        for x in range(190, 640, 75):#sets a x-range for mulitple walls(x-range = 190 -> 640)(space between walls = 75)
            for y in range(200, 400, 75):#sets a y-range for mulitple walls(y-range = 200 -> 400)(space between walls = 75)
                wall = Wall(x, y, 50, 50, DARKRED)#creates the walls (width = 50, height = 50, color = DARKRED)
                self.wall_list.add(wall)#adds the wall to the wall_list

        for x in range(265, 565, 75):#sets a x-range for mulitple walls(x-range = 265 -> 565)(space between walls = 75)
            wall = Wall(x, 275, 50, 50, DARKPURPLE)#creates the walls (width = 50, height = 50, color = DARKPURPLE)
            self.wall_list.add(wall)#adds the wall to the wall_list
        
class Room4(Room):#creates room4 and the walls found in it

    #calls parent contructer
    def __init__(self):
        super().__init__()
 
         #list of walls([x, y, width, height])
        walls = [[0, 0, 20, 250, WHITE],
                 [0, 350, 20, 250, WHITE],
                 [780, 0, 20, 250, WHITE],
                 [780, 350, 20, 250, WHITE],
                 
                 [20, 0, 350, 20, WHITE],
                 [370, 0, 20, 20, WHITE],
                 
                 [410, 0, 20, 20, WHITE],
                 [430, 0, 350, 20, WHITE],
                 
                 [20, 580, 360, 20, WHITE],
                 [370, 580, 20, 20, WHITE],
                 
                 [430, 580, 350, 20, WHITE],
                 [410, 580, 20, 20, WHITE],
                 
                 [35, 100, 730, 5, BLACK],
                 [20, 170, 370, 5, BLACK],
                 [410, 170, 370, 5, BLACK],
                 
                 [370, 160, 20, 20, WHITE],
                 [410, 160, 20, 20, WHITE],
                 
                 [35, 500, 730, 5, BLACK],
                 [20, 430, 370, 5, BLACK],
                 [410, 430, 370, 5, BLACK],
                 
                 [370, 425, 20, 20, WHITE],
                 [410, 425, 20, 20, WHITE],
                 
                ]
 
        for item in walls:#loops through each wall
            wall = Wall(item[0], item[1], item[2], item[3], item[4])#creates the wall
            self.wall_list.add(wall)#adds the wall to the wall list created in the base class

        for x in range(35, 750, 75):#sets a x-range for mulitple walls(x-range = 35 -> 750)(space between walls = 75)
            for y in range(60, 600, 130):#sets a y-range for mulitple walls(y-range = 60 -> 600)(space between walls = 130)
                wall = Wall(x, y, 55, 5, WHITE)#creates the walls (width = 55, height = 5, color = WHITE)
                self.wall_list.add(wall)#adds the wall to the wall_list
                
        for x in range(35, 750, 75):#sets a x-range for mulitple walls(x-range = 35 -> 750)(space between walls = 75)
            for y in range(20, 600, 130):#sets a y-range for mulitple walls(y-range = 20 -> 600)(space between walls = 130)
                wall = Wall(x, y, 55, 5, WHITE)#creates the walls (width = 55, height = 5, color = WHITE)
                self.wall_list.add(wall)#adds the wall to the wall_list

class Room5(Room):#creates room5 and the walls found in it

    #calls parent contructer
    def __init__(self):
        super().__init__()
 
         #list of walls([x, y, width, height])
        walls = [[0, 0, 20, 170, DARKPURPLE],#side exits
                 [0, 194, 20, 12, DARKPURPLE],#side exits
                 [0, 250, 20, 350, DARKPURPLE],#side exits
                 
                 [780, 0, 20, 170, DARKPURPLE],#side exits
                 [780, 194, 20, 12, DARKPURPLE],#side exits
                 [780, 250, 20, 350, DARKPURPLE],#side exits
                 
                 [20, 0, 340, 20, DARKPURPLE],
                 [440, 0, 340, 20, DARKPURPLE],
                 
                 [0, 580, 390, 20, DARKPURPLE], #entrance to room
                 [410, 580, 390, 20, DARKPURPLE], #entrance to room
                 
                 [350, 100, 100, 30, BLUE],
                 [350, 130, 30, 40, BLUE],
                 [420, 130, 30, 40, BLUE],
                 
                 [330, 80, 140, 4, PURPLE],
                 [330, 80, 4, 90, PURPLE],
                 [20, 166, 310, 4, PURPLE],
                 [466, 80, 4, 90, PURPLE],
                 [470, 166, 310, 4, PURPLE],
                 
                 [330, 300, 60, 4, PURPLE],
                 [410, 300, 60, 4, PURPLE],
                 
                 [330, 400, 60, 4, PURPLE],
                 [410, 400, 60, 4, PURPLE],
                 
                 [330, 300, 4, 280, PURPLE],#entrance walls
                 [466, 300, 4, 280, PURPLE],#entrance walls
                 
                 [20, 204, 760, 2, PURPLE],#middle tube
                 [20, 250, 760, 2, PURPLE],#middle tube
                 
                 [20, 194, 760, 2, BLUE],#top outer middle tube
                 
                 [20, 260, 760, 2, BLUE],#bottom outer middle tube
                 
                 [660, 380, 20, 20, WHITE],
                 [640, 400, 20, 20, WHITE],
                 [620, 420, 20, 20, WHITE],
                 [600, 440,20, 20, WHITE],
                 
                 [580, 420,2, 60, WHITE],
                 [580, 478,60, 2, WHITE],
                 
                 [120, 380, 20, 20, WHITE],
                 [140, 400, 20, 20, WHITE],
                 [160, 420, 20, 20, WHITE],
                 [180, 440,20, 20, WHITE],
                 
                 [218, 420,2, 60, WHITE],
                 [160, 478,60, 2, WHITE], 
                ]
        
        for item in walls:#loops through each wall
            wall = Wall(item[0], item[1], item[2], item[3], item[4])#creates the wall
            self.wall_list.add(wall)#adds the wall to the wall list created in the base class
        
class Room6(Room):#creates room6 and the walls inside of it

    #calls parent contructer
    def __init__(self):
        super().__init__()
 
         #list of walls([x, y, width, height])
        walls = [[0, 0, 20, 600, BLACK],
                 [780, 0, 20, 600, BLACK],
                 
                 [20, 0, 370, 20, BLACK],
                 [410, 0, 370, 20, BLACK],
                 
                 [35, 580, 355, 20, BLACK],
                 [410, 580, 390, 20, BLACK],
                 
                 [100, 50, 290, 5, WHITE],
                 [410, 50, 290, 5, WHITE],
                 [100, 105, 600, 5, WHITE],
                 [100, 55, 5, 50, WHITE],
                 [695, 55, 5, 50, WHITE],
                 [415, 20, 5, 30, WHITE],#exit
                 [380, 20, 5, 30, WHITE],#exit
                 
                 
                 [100, 490, 600, 5, WHITE],
                 [100, 495, 5, 50, WHITE],
                 [695, 495, 5, 50, WHITE],
                 [100, 545, 290, 5, WHITE],
                 [410, 545, 290, 5, WHITE],
                 [415, 550, 5, 30, WHITE],#exit
                 [380, 550, 5, 30, WHITE],#exit
                ]
                 
        for item in walls:#loops through each wall
            wall = Wall(item[0], item[1], item[2], item[3], item[4])#creates the wall
            self.wall_list.add(wall)#adds the wall to the wall list created in the base class
            
class Room7(Room):#creates room7 and the walls inside of it

    #calls parent contructer
    def __init__(self):
        super().__init__()
 
         #list of walls([x, y, width, height])
        walls = [[150, 0, 20, 290, RED],#left side
                 [150, 310, 20, 290, RED],#left side
                 [630, 0, 20, 290, RED],#right side
                 [630, 310, 20, 290, RED],#right side
                 
                 [650, 270, 150, 20, RED],#right side
                 [650, 310, 150, 20, RED],#right side
                 
                 [0, 270, 150, 20, RED],#left side
                 [0, 310, 150, 20, RED],#left side
                
                 [390, 20, 20, 560, RED],#middle side
                 
                 [0, 0, 390, 20, BLACK],#top side
                 [410, 0, 390, 20, BLACK],#top side
                 [0, 580, 390, 20, BLACK],#bottom side
                 [410, 580, 390, 20, BLACK],#bottom side
                ]
                 
        for item in walls:#loops through each wall
            wall = Wall(item[0], item[1], item[2], item[3], item[4])#creates the wall
            self.wall_list.add(wall)#adds the wall to the wall list created in the base class

class Room8(Room):#creates room8 and the walls inside of it

    #calls parent contructer
    def __init__(self):
        super().__init__()
 
         #list of walls([x, y, width, height])
        walls = [[0, 20, 20, 60, BROWN],
                 [0, 0, 440, 20, BROWN],#top side top tunnel
                 [0, 80, 360, 20, BROWN],#bottom side top tunnel
                 
                 [360, 80, 20, 500, BROWN],#left side middle tunnel
                 [440, 0, 20, 520, BROWN],#right side middle tunnel
                 
                 [360, 580, 440, 20, BROWN],#bottom side bottom side
                 [440, 500, 360, 20, BROWN],#bottom side top side
                ]
                 
        for item in walls:#loops through each wall
            wall = Wall(item[0], item[1], item[2], item[3], item[4])#creates the wall
            self.wall_list.add(wall)#adds the wall to the wall list created in the base class
            
class Room9(Room):#creates room9 and the walls inside of it

    #calls parent contructer
    def __init__(self):
        super().__init__()
 
         #list of walls([x, y, width, height])
        walls = [[780, 20, 20, 60, BROWN],
                 [360, 0, 440, 20, BROWN],#top side top tunnel
                 [440, 80, 360, 20, BROWN],#bottom side top tunnel
                 
                 [440, 80, 20, 500, BROWN],#left side middle tunnel
                 [360, 0, 20, 520, BROWN],#right side middle tunnel
                 
                 [0, 580, 460, 20, BROWN],#bottom side bottom side
                 [0, 500, 360, 20, BROWN],#bottom side top side
                ]
                 
        
        for item in walls:#loops through each wall
            wall = Wall(item[0], item[1], item[2], item[3], item[4])#creates the wall
            self.wall_list.add(wall)#adds the wall to the wall list created in the base class
            
class Room10(Room):#creates room10 and the walls inside of it

    #calls parent contructer
    def __init__(self):
        super().__init__()
 
         #list of walls([x, y, width, height])
        walls = [[0, 0, 800, 20, WHITE],
                 [0, 20, 20, 580, WHITE],
                 [0, 580, 800, 20, WHITE],
                 [780, 20, 20, 580, WHITE],
                 
                 [100, 40, 2, 540, WHITE],
                 [122, 20, 2, 540, WHITE],
                 [144, 40, 2, 540, WHITE],
                 [166, 20, 2, 540, WHITE],
                 [188, 40, 2, 540, WHITE],
                 [210, 20, 2, 540, WHITE],
                 
                 [698, 40, 2, 540, WHITE],
                 [676, 20, 2, 540, WHITE],
                 [654, 40, 2, 540, WHITE],
                 [632, 20, 2, 540, WHITE],
                 [610, 40, 2, 540, WHITE],
                 [588, 20, 2, 540, WHITE],
                 
                 [232, 400, 334, 2, WHITE],
                 [232, 485, 334, 2, WHITE],
                 
                 [232, 412, 104.5, 5, WHITE],#E
                 [232, 417, 5, 20, WHITE],#E
                 [232, 437, 104.5, 5, WHITE],#E
                 [232, 452, 5, 20, WHITE],#E
                 [232, 472, 104.5, 5, WHITE],#E
                 
                 [346.5, 412, 5, 65, WHITE],#N
                 [346.5, 417, 104.5, 5, WHITE],#N
                 [445, 422, 5, 55, WHITE],#N
                 
                 [461, 412, 99.5, 5, WHITE],#D
                 [461, 472, 99.5, 5, WHITE],#D
                 [461, 417, 5, 55, WHITE],#D
                 [560.5, 417, 5, 55, WHITE],#D
                 
                 [232, 40, 334, 300, BLUE],#blue block
                ]
                 
        for item in walls:#loops through each wall
            wall = Wall(item[0], item[1], item[2], item[3], item[4])#creates the wall
            self.wall_list.add(wall)#adds the wall to the wall list created in the base class


def main():#define the main program

    pygame.init()#initializes pygame
 
    screen = pygame.display.set_mode([800, 600])#Creates an 800x600 sized screen
 
    pygame.display.set_caption('THE MAZE OF CONFUSION')#Set the title of the window
    
    player = Player(700, 292.5)#Coordinates at which player starts
    movingsprites = pygame.sprite.Group()
    movingsprites.add(player)#add player sprite to moving sprites

    rooms = []#creates a list of rooms
 
    #creates the rooms and adds them to the rooms list 
    room = Room1()
    rooms.append(room)
    room = Room2()
    rooms.append(room)
    room = Room3()
    rooms.append(room)
    room = Room4()
    rooms.append(room)
    room = Room5()
    rooms.append(room)
    room = Room6()
    rooms.append(room)
    room = Room7()
    rooms.append(room)
    room = Room8()
    rooms.append(room)
    room = Room9()
    rooms.append(room)
    room = Room10()
    rooms.append(room)
    
    current_room_no = 0#set current_room_no equal to 0
    current_room = rooms[current_room_no]#set current_room equal to the room # that we are in
 
    clock = pygame.time.Clock()#manages how fast the screen updates(fps)
 
    done = False#loops until the user closes the game

    while not done:#while game is playing (not closed)
 
        for event in pygame.event.get():
            if event.type == pygame.QUIT:#If the close button is pressed
                done = True#Then game will close
         
            #When user presses on the movement keys, changespeed increases or decreases depending on the key
            if event.type == pygame.KEYDOWN:#if a key is pressed down
                if event.key == pygame.K_a:#if the key is a
                    player.changespeed(-5, 0)#Then changespeed's x-value decreases by 5 = moves to the left
                if event.key == pygame.K_d:#if the key is d
                    player.changespeed(5, 0)#Then changespeed's x-value increases by 5 = moves to the right
                if event.key == pygame.K_w:#if the key is w
                    player.changespeed(0, -5)#Then changespeed's y-value decreases by 5 = moves up
                if event.key == pygame.K_s:#if the key is s
                    player.changespeed(0, 5)#Then changespeed's y-value increases by 5 = moves down
 
            #When user stops pressing on the movement keys, speed goes back to 0 (player stops)
            if event.type == pygame.KEYUP:#if user lets go of a key
                if event.key == pygame.K_a:#if the key is a
                    player.changespeed(5, 0)#Then changespeed's x-value returns to 0 = no movement to the left
                if event.key == pygame.K_d:#if the key is d
                    player.changespeed(-5, 0)#Then changespeed's x-value returns to 0 = no movement to the right
                if event.key == pygame.K_w:#if the key is w
                    player.changespeed(0, 5)#Then changespeed's y-value returns to 0 = no upwards movement
                if event.key == pygame.K_s:#if the key is s
                    player.changespeed(0, -5)#Then changespeed's y-value returns to 0 = no downwards movement
 
        player.move(current_room.wall_list)#

        if player.rect.x < -10:#if player x-coordinate is below -10 
            if current_room_no == 0:#if player is in room1
                current_room_no = 2#Then player will go to room 3
                current_room = rooms[current_room_no]
                player.rect.x = 790#the players x-coordinate will be 790
            elif current_room_no == 1:#if player is in room2
                current_room_no = 0#Then player will go to room 1
                current_room = rooms[current_room_no]
                player.rect.x = 790#the players x-coordinate will be 790
            elif current_room_no == 2:#if player is in room3
                current_room_no = 3#Then player will go to room 4
                current_room = rooms[current_room_no]
                player.rect.x = 790#the players x-coordinate will be 790
            elif current_room_no == 3:#if player is in room4
                current_room_no = 1#Then player will go to room 2
                current_room = rooms[current_room_no]
                player.rect.x = 700#the players x-coordinate will be 700
            #note = (room 4 top tunnel left side -> room10) 
            elif current_room_no == 4:#if player is in room5
                current_room_no = 9#Then player will go to room10
                current_room = rooms[current_room_no]
                player.rect.x = 50#the players x-coordinate will be 50
                player.rect.y = 550#the players y-coordinate will be 550
            elif current_room_no == 6:#if player is in room7
                current_room_no = 8#Then player will go to room9
                current_room = rooms[current_room_no]
                player.rect.x = 750#the players x-coordinate will be 750
                player.rect.y = 50#the players y-coordinate will be 50
                
#note = (bottom left room 1 to top room 6)
        if player.rect.x < 5:#if player x-coordinate is below 5
            if player.rect.y > 539:#if player y-coordinate is above 539
                if current_room_no == 0:#if player is in room1
                    current_room_no = 5#Then player will go to room6
                    current_room = rooms[current_room_no]
                    player.rect.x = 392.5#the players x-coordinate will be 392.5
                    player.rect.y = 60#the players y-coordinate will be 60
                    
#note = (room 9 to room1)
        if player.rect.x < 15:#if player x-coordinate is below 15
            if player.rect.y > 500:#if player y-coordinate is above 500
                if current_room_no == 8:#if player is in room9
                    current_room_no = 0#Then player will go to room1
                    current_room = rooms[current_room_no]
                    player.rect.y = 550#the players x-coordinate will be 550
                    player.rect.x = 750#the players y-coordinate will be 750

#note = (top right room 1 to bottom room 6)
        if player.rect.x > 790:#if player x-coordinate is above 790
            if player.rect.y < 60:#if player y-coordinate is below 60
                if current_room_no == 0:#if player is in room1
                    current_room_no = 5#Then player will go to room6
                    current_room = rooms[current_room_no]
                    player.rect.x = 392.5#the players x-coordinate will be 392.5
                    player.rect.y = 500#the players y-coordinate will be 500
 
        if player.rect.x > 801:#if player x-coordinate is above 801
            if current_room_no == 0:#if player is in room1
                current_room_no = 1#Then player will go to room2
                current_room = rooms[current_room_no]
                player.rect.x = 0#the players x-coordinate will be 0
            elif current_room_no == 1:#if player is in room2
                current_room_no = 2#Then player will go to room3
                current_room = rooms[current_room_no]
                player.rect.x = 0#the players x-coordinate will be 0
            elif current_room_no == 2:#if player is in room3
                current_room_no = 0#Then player will go to room1
                current_room = rooms[current_room_no]
                player.rect.x = 0#the players x-coordinate will be 0
            #note = (room 4 top tunnel right side -> room 10)
            elif current_room_no == 4:#if player is in room5
                current_room_no = 9#Then player will go to room10
                current_room = rooms[current_room_no]
                player.rect.x = 50#the players x-coordinate will be 50
                player.rect.y = 550#the players y-coordinate will be 550
            elif current_room_no == 6:#if player is in room7
                current_room_no = 7#Then player will go to room8
                current_room = rooms[current_room_no]
                player.rect.x = 50#the players x-coordinate will be 50
                player.rect.y = 50#the players y-coordinate will be 50
                
#note = (room 5 bottom tunnel right side to room 7)
        if player.rect.x > 795:#if player x-coordinate is above 795
            if player.rect.y > 206:#if player y-coordinate is above 206
                if current_room_no == 4:#if player is in room5
                    current_room_no = 6#Then player will go to room7
                    current_room = rooms[current_room_no]
                    player.rect.x = 250#the players x-coordinate will be 250
                    player.rect.y = 292.5#the players y-coordinate will be 292.5
                    
#note = (room 5 bottom tunnel left side to room 7)            
        if player.rect.x < 0:#if player x-coordinate is below 0
            if player.rect.y > 206:#if player y-coordinate is above 206
                if current_room_no == 4:#if player is in room5
                    current_room_no = 6#Then player will go to room7
                    current_room = rooms[current_room_no]
                    player.rect.x = 450#the players x-coordinate will be 450
                    player.rect.y = 292.5#the players y-coordinate will be 292.5
        
        if player.rect.y < -15:#if player y-coordinate is below -15
            if current_room_no == 3:#if player is in room4
                current_room_no = 4#Then player will go to room5
                current_room = rooms[current_room_no]
                player.rect.y = 280#the players y-coordinate will be 280
                player.rect.x = 392.5#the players x-coordinate will be 392.5
            elif current_room_no == 4:#if player is in room5
                current_room_no = 3#Then player will go to room4
                current_room = rooms[current_room_no]
                player.rect.y = 580#the players y-coordinate will be 580
            #note= (top room 6 -> room 1)
            elif current_room_no == 5:#if player is in room6
                current_room_no = 0#Then player will go to room1
                current_room = rooms[current_room_no]
                player.rect.y = 150#the players y-coordinate will be 150
                player.rect.x = 150#the players x-coordinate will be 150

        if player.rect.y > 600:#if player y-coordinate is above 600
            if current_room_no == 3:#if player is in room4
                current_room_no = 4#Then player will go to room5
                current_room = rooms[current_room_no]
                player.rect.y = 50#the players y-coordinate will be 50
                player.rect.x = 392.5#the players x-coordinate will be 392.5
            elif current_room_no == 4:#if player is in room5
                current_room_no = 5#Then player will go to room6
                current_room = rooms[current_room_no]
                player.rect.y = 150#the players y-coordinate will be 150
                player.rect.x = 392.5#the players x-coordinate will be 392.5
            #note = (bottom room 6 -> top tunnel room 5)
            elif current_room_no == 5:#if player is in room6
                current_room_no = 4#Then player will go to room5
                current_room = rooms[current_room_no]
                player.rect.y = 140#the players y-coordinate will be 140
                player.rect.x = 392.5#the players x-coordinate will be 392.5
     
#note = (bottom left room 6 to middle room 5)         
        if player.rect.y > 595:#if player y-coordinate is above 595
            if player.rect.x < 60:#if player x-coordinate is below 60
                if current_room_no == 5:#if player is in room6
                    current_room_no = 4 #Then player will go to room5
                    current_room = rooms[current_room_no]
                    player.rect.y = 212#the players y-coordinate will be 212
                    player.rect.x = 392.5#the players x-coordinate will be 392.5

###room 8 -> 0
        if player.rect.x > 795:#if player x-coordinate is above 795
            if player.rect.y > 500:#if player y-coordinate is above 500
                if current_room_no == 7:#if player is in room8
                    current_room_no = 0#Then player will go to room1
                    current_room = rooms[current_room_no]
                    player.rect.y = 30#the players y-coordinate will be 30
                    player.rect.x = 50#the players x-coordinate will be 50

        screen.fill(BLACK)#sets the background color as black
 
        movingsprites.draw(screen)#draws the player
        current_room.wall_list.draw(screen)#draws all the walls of the current_room on the screen
 
        pygame.display.flip()#updates screen with all the new changes
 
        clock.tick(60)#set max framerate at 60fps
 
    pygame.quit()

#calls the main function
if __name__ == "__main__":
    main()
