# Create-performance-task
"""
Sample Python/Pygame Programs
Simpson College Computer Science
http://programarcadegames.com/
http://simpson.edu/computer-science/
 
From:
http://programarcadegames.com/python_examples/f.php?file=maze_runner.py
 
Explanation video: http://youtu.be/5-SbFanyUkQ
 
Part of a series:
http://programarcadegames.com/python_examples/f.php?file=move_with_walls_example.py
http://programarcadegames.com/python_examples/f.php?file=maze_runner.py
http://programarcadegames.com/python_examples/f.php?file=platform_jumper.py
http://programarcadegames.com/python_examples/f.php?file=platform_scroller.py
http://programarcadegames.com/python_examples/f.php?file=platform_moving.py
http://programarcadegames.com/python_examples/sprite_sheets/
"""

import pygame
 

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

import random

def random_color():
    levels = range(32,256,32)
    return tuple(random.choice(levels) for _ in range(3))


"""
note in this code the height is 600 and the width is 
800 and coordinates 0,0 are bottom left
"""
 
 
class Wall(pygame.sprite.Sprite):
    """This class represents the bar at the bottom that the player controls """
 
    def __init__(self, x, y, width, height, color):
        """ Constructor function """
 
        # Call the parent's constructor
        super().__init__()
 
        # Make a BLUE wall, of the size specified in the parameters
        self.image = pygame.Surface([width, height])
        self.image.fill(color)
 
        # Make our top-left corner the passed-in location.
        self.rect = self.image.get_rect()
        self.rect.x = x
        self.rect.y = y
        #self.rect.bottomleft = (0, 0) # set bottom left

 
class Player(pygame.sprite.Sprite):
    """ This class represents the bar at the bottom that the
    player controls """
 
    # Set speed vector
    change_x = 0
    change_y = 0
 
    def __init__(self, x, y):
        """ Constructor function """
 
        # Call the parent's constructor
        super().__init__()
 
        # Set height, width
        self.image = pygame.Surface([15, 15])
        self.image.fill(random_color())
 
        # Make our top-left corner the passed-in location.
        self.rect = self.image.get_rect()
        self.rect.y = y
        self.rect.x = x
 
    def changespeed(self, x, y):
        """ Change the speed of the player. Called with a keypress. """
        self.change_x += x
        self.change_y += y
 
    def move(self, walls):
        """ Find a new position for the player """
 
        # Move left/right
        self.rect.x += self.change_x
 
        # Did this update cause us to hit a wall?
        block_hit_list = pygame.sprite.spritecollide(self, walls, False)
        for block in block_hit_list:
            # If we are moving right, set our right side to the left side of
            # the item we hit
            if self.change_x > 0:
                self.rect.right = block.rect.left
            else:
                # Otherwise if we are moving left, do the opposite.
                self.rect.left = block.rect.right
 
        # Move up/down
        self.rect.y += self.change_y
 
        # Check and see if we hit anything
        block_hit_list = pygame.sprite.spritecollide(self, walls, False)
        for block in block_hit_list:
 
            # Reset our position based on the top/bottom of the object.
            if self.change_y > 0:
                self.rect.bottom = block.rect.top
            else:
                self.rect.top = block.rect.bottom

class Player2(pygame.sprite.Sprite):
    """ This class represents the bar at the bottom that the
    player controls """
 
    # Set speed vector
    change_x = 0
    change_y = 0
 
    def __init__(self, x, y):
        """ Constructor function """
 
        # Call the parent's constructor
        super().__init__()
 
        # Set height, width
        self.image = pygame.Surface([10, 10])
        self.image.fill(random_color())
 
        # Make our top-left corner the passed-in location.
        self.rect = self.image.get_rect()
        self.rect.y = y
        self.rect.x = x
 
    def changespeed(self, x, y):
        """ Change the speed of the player. Called with a keypress. """
        self.change_x += x
        self.change_y += y
 
    def move(self, walls):
        """ Find a new position for the player """
 
        # Move left/right
        self.rect.x += self.change_x
 
        # Did this update cause us to hit a wall?
        block_hit_list = pygame.sprite.spritecollide(self, walls, False)
        for block in block_hit_list:
            # If we are moving right, set our right side to the left side of
            # the item we hit
            if self.change_x > 0:
                self.rect.right = block.rect.left
            else:
                # Otherwise if we are moving left, do the opposite.
                self.rect.left = block.rect.right
 
        # Move up/down
        self.rect.y += self.change_y
 
        # Check and see if we hit anything
        block_hit_list = pygame.sprite.spritecollide(self, walls, False)
        for block in block_hit_list:
 
            # Reset our position based on the top/bottom of the object.
            if self.change_y > 0:
                self.rect.bottom = block.rect.top
            else:
                self.rect.top = block.rect.bottom
 
class Room(object):
    """ Base class for all rooms. """
 
    # Each room has a list of walls, and of enemy sprites.
    wall_list = None
    enemy_sprites = None
 
    def __init__(self):
        """ Constructor, create our lists. """
        self.wall_list = pygame.sprite.Group()
        self.enemy_sprites = pygame.sprite.Group()
        

class Room1(Room):
    """This creates all the walls in room 1"""
    def __init__(self):
        super().__init__()
        # Make the walls. (x_pos, y_pos, width, height)
 
        # This is a list of walls. Each is in the form [x, y, width, height]
        walls = [[0, 0, 20, 250, TURQUOISE],
                 [0, 350, 20, 250, TURQUOISE],
                 [780, 0, 20, 250, TURQUOISE],
                 [780, 350, 20, 250, TURQUOISE],
                 [20, 0, 760, 20, TURQUOISE],
                 [20, 580, 760, 20, TURQUOISE],
                 [390, 50, 20, 500, BLUE],
                 [190, 50, 20, 500, BLUE],
                 [590, 50, 20, 500, BLUE],
                 [235, 290, 130, 20, LIGHTBLUE],
                 [435, 290, 130, 20, LIGHTBLUE],
                 [290, 20, 20, 200, GREY],
                 [490, 20, 20, 200, GREY],
                 [290, 380, 20, 200, GREY],
                 [490, 380, 20, 200, GREY],
                 [20, 115, 100, 20, PURPLE],
                 [20, 450, 100, 20, PURPLE],
                 [680, 115, 100, 20, PURPLE],
                 [680, 450, 100, 20, PURPLE]
                ]
    
        # Loop through the list. Create the wall, add it to the list
        for item in walls:
            wall = Wall(item[0], item[1], item[2], item[3], item[4])
            self.wall_list.add(wall)
        
class Room2(Room):
    """This creates all the walls in room 2"""
    def __init__(self):
        super().__init__()
 
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
 
        for item in walls:
            wall = Wall(item[0], item[1], item[2], item[3], item[4])
            self.wall_list.add(wall)

class Room3(Room):
    """This creates all the walls in room 3"""
    def __init__(self):
        super().__init__()
 
        walls = [[0, 0, 20, 250, BRIGHTYELLOW],
                 [0, 350, 20, 250, BRIGHTYELLOW],
                 [780, 0, 20, 250, BRIGHTYELLOW],
                 [780, 350, 20, 250, BRIGHTYELLOW],
                 [20, 0, 760, 20, BRIGHTYELLOW],
                 [20, 580, 760, 20, BRIGHTYELLOW],
                ]
 
        for item in walls:
            wall = Wall(item[0], item[1], item[2], item[3], item[4])
            self.wall_list.add(wall)
 
    
        for x in range(40, 750, 75):
            for y in range(50, 550, 75):
                wall = Wall(x, y, 50, 50, ORANGE)
                self.wall_list.add(wall)
 
        for x in range(115, 700, 75):
            for y in range(125, 500, 75):
                wall = Wall(x, y, 50, 50, RED)
                self.wall_list.add(wall)

        for x in range(190, 640, 75):
            for y in range(200, 400, 75):
                wall = Wall(x, y, 50, 50, DARKRED)
                self.wall_list.add(wall)

        for x in range(265, 565, 75):
            wall = Wall(x, 275, 50, 50, DARKPURPLE)
            self.wall_list.add(wall)
        
class Room4(Room):
    """This creates all the walls in room 4"""
    def __init__(self):
        super().__init__()
 
        walls = [[0, 0, 20, 250, WHITE],
                 [0, 350, 20, 250, WHITE],
                 [780, 0, 20, 250, WHITE],
                 [780, 350, 20, 250, WHITE],
                 [20, 0, 360, 20, WHITE],
                 [420, 0, 360, 20, WHITE],
                 [20, 580, 360, 20, WHITE],
                 [420, 580, 360, 20, WHITE],
                ]
 
        for item in walls:
            wall = Wall(item[0], item[1], item[2], item[3], item[4])
            self.wall_list.add(wall)

                
        for x in range(60, 750, 75):
            for y in range(20, 560, 130):
                wall = Wall(x, y, 5, 45, WHITE)
                self.wall_list.add(wall)
        
        for x in range(35, 750, 75):
            for y in range(60, 600, 130):
                wall = Wall(x, y, 55, 5, WHITE)
                self.wall_list.add(wall)
                
        for x in range(35, 750, 75):
            for y in range(20, 600, 130):
                wall = Wall(x, y, 55, 5, WHITE)
                self.wall_list.add(wall)

class Room5(Room):
    """This creates all the walls in room 5"""
    def __init__(self):
        super().__init__()
 
        walls = [[0, 0, 20, 600, DARKPURPLE],
                 [780, 0, 20, 600, DARKPURPLE],
                 [20, 0, 780, 20, DARKPURPLE],
                 
                 [0, 580, 390, 20, DARKPURPLE], #entrance to room
                 [410, 580, 390, 20, DARKPURPLE], #entrance to room
                 
                 [350, 100, 100, 100, BLUE],
                 [330, 80, 140, 4, PURPLE],
                 [330, 80, 4, 140, PURPLE],
                 [466, 80, 4, 142, PURPLE],
                 
                 [330, 220, 60, 4, PURPLE],#entrance to portal1
                 [410, 220, 60, 4, PURPLE],#entrance to portal1
                 
                 [330, 250, 60, 4, PURPLE],#entrance to portal1
                 [410, 250, 60, 4, PURPLE],#entrance to portal1
                
                 [330, 300, 60, 4, PURPLE],#entrance to portal1
                 [410, 300, 60, 4, PURPLE],#entrance to portal1
                 
                 [330, 400, 60, 4, PURPLE],#entrance to portal1
                 [410, 400, 60, 4, PURPLE],#entrance to portal1
                 
                 [280, 220, 50, 4, PURPLE],#entrance to portal2/3
                 [466, 220, 50, 4, PURPLE],#entrance to portal2/3
                 
                 [280, 250, 50, 4, PURPLE],#entrance to portal2/3
                 [466, 250, 50, 4, PURPLE],#entrance to portal2/3
                 
                 
                 [180, 170, 100, 50, DARKPURPLE],
                 [180, 254, 100, 50, DARKPURPLE],
                 [180, 170, 20, 100, DARKPURPLE],
                 
                 [179, 170, 1, 133, BLUE],
                 [180, 169, 100, 1, BLUE],
                 [180, 302, 100, 1, BLUE],
                 
                 [515, 170, 100, 50, DARKPURPLE],
                 [515, 254, 100, 50, DARKPURPLE],
                 [595, 170, 20, 100, DARKPURPLE],
                 
                 [614, 170, 1, 133, BLUE],
                 [515, 169, 100, 1, BLUE],
                 [515, 302, 100, 1, BLUE],
                 
                 [200, 220, 4, 33, BLUE],
                 [595, 220, 4, 34, BLUE],
                 
                 [200, 220, 80, 4, BLUE],
                 [200, 250, 80, 4, BLUE],
                 
                 [516, 220, 80, 4, BLUE],
                 [516, 250, 80, 4, BLUE],
                 
                 [330, 220, 4, 0, PURPLE],
                 [466, 220, 4, 0, PURPLE],
                 
                 [330, 250, 4, 330, PURPLE],
                 [466, 250, 4, 330, PURPLE],
                ]
        
        for item in walls:
            wall = Wall(item[0], item[1], item[2], item[3], item[4])
            self.wall_list.add(wall)
        

class Room6(Room):
    """This creates all the walls in room 5"""
    def __init__(self):
        super().__init__()
 
        walls = [[0, 0, 20, 600, WHITE],
                 [780, 0, 20, 600, WHITE],
                 [20, 0, 780, 20, WHITE],
                 
                 [0, 580, 390, 20, WHITE],
                 [410, 580, 390, 20, WHITE],
                 
                 [350, 100, 100, 100, BLUE],
                 [330, 80, 140, 2, PURPLE],
                 [330, 80, 2, 140, PURPLE],
                 [470, 80, 2, 142, PURPLE],
                 [330, 220, 60, 2, PURPLE],
                 [410, 220, 60, 2, PURPLE],
                ]
        
        for item in walls:
            wall = Wall(item[0], item[1], item[2], item[3], item[4])
            self.wall_list.add(wall)

def main():
    """ Main Program """
 
    # Call this function so the Pygame library can initialize itself
    pygame.init()
 
    # Create an 800x600 sized screen
    screen = pygame.display.set_mode([1000, 800])
 
    # Set the title of the window
    pygame.display.set_caption('THE MAZE')
 
    # Create the player paddle object
   
    player = Player(50, 50)
    movingsprites = pygame.sprite.Group()
    movingsprites.add(player)
    
    player2 = Player(500, 50)
    movingsprites = pygame.sprite.Group()
    movingsprites.add(player)
 
    rooms = []
 
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
    
    current_room_no = 0
    current_room = rooms[current_room_no]
 
    clock = pygame.time.Clock()
 
    done = False
 
    while not done:
 
        # --- Event Processing ---
 
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                done = True
 
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_a:
                    player.changespeed(-5, 0)
                if event.key == pygame.K_d:
                    player.changespeed(5, 0)
                if event.key == pygame.K_w:
                    player.changespeed(0, -5)
                if event.key == pygame.K_s:
                    player.changespeed(0, 5)
 
            if event.type == pygame.KEYUP:
                if event.key == pygame.K_a:
                    player.changespeed(5, 0)
                if event.key == pygame.K_d:
                    player.changespeed(-5, 0)
                if event.key == pygame.K_w:
                    player.changespeed(0, 5)
                if event.key == pygame.K_s:
                    player.changespeed(0, -5)
                    
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    player2.changespeed(-5, 0)
                if event.key == pygame.K_RIGHT:
                    player2.changespeed(5, 0)
                if event.key == pygame.K_UP:
                    player2.changespeed(0, -5)
                if event.key == pygame.K_DOWN:
                    player2.changespeed(0, 5)
 
            if event.type == pygame.KEYUP:
                if event.key == pygame.K_LEFT:
                    player2.changespeed(5, 0)
                if event.key == pygame.K_RIGHT:
                    player2.changespeed(-5, 0)
                if event.key == pygame.K_UP:
                    player2.changespeed(0, 5)
                if event.key == pygame.K_DOWN:
                    player2.changespeed(0, -5)
 
        # --- Game Logic ---
 
        player.move(current_room.wall_list)
 
        if player.rect.x < -15:
            if current_room_no == 0:
                current_room_no = 3
                current_room = rooms[current_room_no]
                player.rect.x = 790
            elif current_room_no == 3:
                current_room_no = 2
                current_room = rooms[current_room_no]
                player.rect.x = 790
            elif current_room_no == 2:
                current_room_no = 1
                current_room = rooms[current_room_no]
                player.rect.x = 790
            else:
                current_room_no = 0
                current_room = rooms[current_room_no]
                player.rect.x = 790
 
        if player.rect.x > 801:
            if current_room_no == 0:
                current_room_no = 1
                current_room = rooms[current_room_no]
                player.rect.x = 0
            elif current_room_no == 1:
                current_room_no = 2
                current_room = rooms[current_room_no]
                player.rect.x = 0
            else:
                current_room_no = 0
                current_room = rooms[current_room_no]
                player.rect.x = 0
            
        if player.rect.y < -15:
            if current_room_no == 3:
                current_room_no = 4
                current_room = rooms[current_room_no]
                player.rect.y = 590
            else:
                current_room_no = 0
                current_room = rooms[current_room_no]
                player.rect.y = 0

        player2.move(current_room.wall_list)
        
        if player2.rect.x < -15:
            if current_room_no == 0:
                current_room_no = 2
                current_room = rooms[current_room_no]
                player2.rect.x = 790
            elif current_room_no == 2:
                current_room_no = 1
                current_room = rooms[current_room_no]
                player2.rect.x = 790
            else:
                current_room_no = 0
                current_room = rooms[current_room_no]
                player2.rect.x = 790
 
        if player2.rect.x > 801:
            if current_room_no == 0:
                current_room_no = 1
                current_room = rooms[current_room_no]
                player2.rect.x = 0
            elif current_room_no == 1:
                current_room_no = 2
                current_room = rooms[current_room_no]
                player2.rect.x = 0
            else:
                current_room_no = 0
                current_room = rooms[current_room_no]
                player2.rect.x = 0

        # --- Drawing ---
        screen.fill(BLACK)
 
        movingsprites.draw(screen)
        current_room.wall_list.draw(screen)
 
        pygame.display.flip()
 
        clock.tick(60)
 
    pygame.quit()


if __name__ == "__main__":
    main()



