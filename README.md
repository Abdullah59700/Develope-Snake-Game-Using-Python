
# Develope-Snake-Game-Using-Python
Snake Game - Python Project I developed a classic Snake game using Python and the pygame library as part of my exploration into game development. This project showcases my skills in programming, real-time user input handling, and creating interactive applications.

# Key Learnings:

- Understanding the intricacies of game loops and event handling.
- Implementing real-time user inputs for a seamless gaming experience.
- Balancing game difficulty to keep it both fun and challenging.

 # Libraries Used:
- Pygame: The backbone of this project, Pygame provided the essential tools for handling graphics, sounds, and game states.
- Random: Utilized to generate random positions for the snake’s food, adding an unpredictable element to the game.
- Time: Managed game speed and ensured smooth transitions between frames.

----


 - # Import Libraries.
```
import pygame
import time
import random
```
 - # Initialize Pygame

```
pygame.init()
```
 - # Define colors
  
```
white = (255, 255, 255)
yellow = (255, 255, 102)
black = (0, 0, 0)
red = (213, 50, 80)
green = (0, 255, 0)
blue = (50, 153, 213)
```

 - # Set display dimensions
  
```
width = 600
height = 400
display = pygame.display.set_mode((width, height))
pygame.display.set_caption('Snake Game Created By: Abdullah Jamil.')
```

 - # Set game clock
  
```
clock = pygame.time.Clock()
```

- # Snake parameters
```
snake_block = 10 snake_speed = 20
```

- # Font styles & Game code. 
 
```
font_style = pygame.font.SysFont("bahnschrift", 25)
score_font = pygame.font.SysFont("comicsansms", 35)

def display_score(score):
    value = score_font.render("Score: " + str(score), True, black)
    display.blit(value, [0, 0])

def draw_snake(snake_block, snake_list):
    for x in snake_list:
        pygame.draw.rect(display, black, [x[0], x[1], snake_block, snake_block])

def message(msg, color):
    mesg = font_style.render(msg, True, color)
    display.blit(mesg, [width / 6, height / 3])

def game_loop():
    game_over = False
    game_close = False

    x1 = width / 2
    y1 = height / 2

    x1_change = 0
    y1_change = 0

    snake_list = []
    length_of_snake = 1

    foodx = round(random.randrange(0, width - snake_block) / 10.0) * 10.0
    foody = round(random.randrange(0, height - snake_block) / 10.0) * 10.0
    while not game_over:

        while game_close == True:
            display.fill(blue)
            message("You Lost!Press C-Play Again or Q-Quit", red)
            display_score(length_of_snake - 1)
            pygame.display.update()

            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:
                        game_loop()

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    x1_change = -snake_block
                    y1_change = 0
                elif event.key == pygame.K_RIGHT:
                    x1_change = snake_block
                    y1_change = 0
                elif event.key == pygame.K_UP:
                    y1_change = -snake_block
                    x1_change = 0
                elif event.key == pygame.K_DOWN:
                    y1_change = snake_block
                    x1_change = 0

        if x1 >= width or x1 < 0 or y1 >= height or y1 < 0:
            game_close = True

        x1 += x1_change
        y1 += y1_change
        display.fill(blue)
        pygame.draw.rect(display, green, [foodx, foody, snake_block, snake_block])
        snake_head = []
        snake_head.append(x1)
        snake_head.append(y1)
        snake_list.append(snake_head)
        if len(snake_list) > length_of_snake:
            del snake_list[0]

        for x in snake_list[:-1]:
            if x == snake_head:
                game_close = True

        draw_snake(snake_block, snake_list)
        display_score(length_of_snake - 1)

        pygame.display.update()

        if x1 == foodx and y1 == foody:
            foodx = round(random.randrange(0, width - snake_block) / 10.0) * 10.0
            foody = round(random.randrange(0, height - snake_block) / 10.0) * 10.0
            length_of_snake += 1

        clock.tick(snake_speed)

    pygame.quit()
    quit()

if __name__ == "__main__":
    try:
        game_loop()
    except Exception as e:
        print(f"An error occurred: {e}")
```

--- 

### **Created By:** **Abdullah Jamil**
### **Date:** 8/19/2024
### **Email**: abdullahdatascientist@gmail.com 
