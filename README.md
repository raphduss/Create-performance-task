# Create-performance-task

# Create-performance-task

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
800 and coordinates 0,0 are top left
"""
 
 
class Wall(pygame.sprite.Sprite):
 
    def __init__(self, x, y, width, height, color):
 
        super().__init__()
 
        self.image = pygame.Surface([width, height])
        self.image.fill(color)
 
        self.rect = self.image.get_rect()
        self.rect.x = x
        self.rect.y = y

 
class Player(pygame.sprite.Sprite):
 
    change_x = 0
    change_y = 0
 
    def __init__(self, x, y):
 
        super().__init__()
 
        self.image = pygame.Surface([15, 15])
        self.image.fill(random_color())
 
        self.rect = self.image.get_rect()
        self.rect.y = y
        self.rect.x = x
 
    def changespeed(self, x, y):
        self.change_x += x
        self.change_y += y
 
    def move(self, walls):
 
        self.rect.x += self.change_x
 
        block_hit_list = pygame.sprite.spritecollide(self, walls, False)
        for block in block_hit_list:
            if self.change_x > 0:
                self.rect.right = block.rect.left
            else:
                # Otherwise if we are moving left, do the opposite.
                self.rect.left = block.rect.right
 
        self.rect.y += self.change_y
        
        block_hit_list = pygame.sprite.spritecollide(self, walls, False)
        for block in block_hit_list:
 
            if self.change_y > 0:
                self.rect.bottom = block.rect.top
            else:
                self.rect.top = block.rect.bottom

class Room(object):
 
    wall_list = None
    enemy_sprites = None
 
    def __init__(self):
        self.wall_list = pygame.sprite.Group()
        self.enemy_sprites = pygame.sprite.Group()
        

class Room1(Room):
    def __init__(self):
        super().__init__()
        # Makes the walls room1 - (x_pos, y_pos, width, height)
 
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
    
        for item in walls:
            wall = Wall(item[0], item[1], item[2], item[3], item[4])
            self.wall_list.add(wall)
        
class Room2(Room):
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
            
class Room6(Room):
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
 
    pygame.init()
 
    screen = pygame.display.set_mode([1000, 800])
 
    pygame.display.set_caption('THE MAZE')
 
   
    player = Player(50, 50)
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
                if event.key == pygame.K_RIGHT:
                    player2.changespeed(-5, 0)
                if event.key == pygame.K_LEFT:
                    player2.changespeed(5, 0)
                if event.key == pygame.K_DOWN:
                    player2.changespeed(0, -5)
                if event.key == pygame.K_UP:
                    player2.changespeed(0, 5)
 
            if event.type == pygame.KEYUP:
                if event.key == pygame.K_RIGHT:
                    player2.changespeed(5, 0)
                if event.key == pygame.K_LEFT:
                    player2.changespeed(-5, 0)
                if event.key == pygame.K_DOWN:
                    player2.changespeed(0, 5)
                if event.key == pygame.K_UP:
                    player2.changespeed(0, -5)
 
 
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

 
        screen.fill(BLACK)
 
        movingsprites.draw(screen)
        current_room.wall_list.draw(screen)
 
        pygame.display.flip()
 
        clock.tick(60)
 
    pygame.quit()


if __name__ == "__main__":
    main()





