# Snake Game
> Basic arcade-style Snake using Python 3 and Pygame.

Learn how to create and MODIFY the infamous Snake Game step by step using the framework library of Pycharm.

<img src="https://media.giphy.com/media/4JmTg4bTuofUQ/source.gif">


## Installation and Dependencies

1. Install Pygame on the command line:

```sh
pip install pygame 
```

2. Import and initialize Pygame into your .py file

## Let's Make the Game

1. Set Screen 
* [x] make use of the display.set_mode() function
* [x] use of the init() and the quit() methods to initialize and uninitialize everything at the start and the end of the code
* [x] use update() method to update any changes made to the screen
* [x] use a while loop before quit() to correct screen time out error
```python 
import pygame
pygame.init()
dis=pygame.display.set_mode((400,300))
pygame.display.update()
game_over=False
while not game_over:
    for event in pygame.event.get():
        if event.type==pygame.QUIT:     #specifies when screen should close out 
            game_over=True         
pygame.quit()
quit()
```

2. Create Snake
* [x] initialize a few color variables in order to color the snake, food, screen, etc.
* [x] Draw rectangles in to make our snake a rectangle using the function called draw.rect()
```python
white = (255, 255, 255)
yellow = (255, 255, 102)
black = (0, 0, 0)
red = (213, 50, 80)
green = (0, 255, 0)
blue = (50, 153, 213)
 
game_over=False
while not game_over:
    for event in pygame.event.get():
        if event.type==pygame.QUIT:
            game_over=True
    pygame.draw.rect(dis,blue,[200,150,10,10])
  ```
3. Move Snake - use key events present in the KEYDOWN class of Pygame.
* [x] use K_UP, K_DOWN, K_LEFT, and K_RIGHT to make the snake move up, down, left and right respectively
* [x] hold the updating values of the x and y coordinates in newX and newY
```python
x1 = 300
y1 = 300
 
newX = 0       
newY = 0
while not game_over:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_over = True
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                newX = -10
                newY = 0
            elif event.key == pygame.K_RIGHT:
                newX = 10
                newY = 0
            elif event.key == pygame.K_UP:
                newY = -10
                newX = 0
            elif event.key == pygame.K_DOWN:
                newY = 10
                newX = 0
 
    x1 += newX
    y1 += newY
   ```
    
4. Game Over Alert
* [x] use an ‘if’ statement that defines the limits for the x and y coordinates of the snake to be less than or equal to that of the screen
```python     if x1 >= dis_width or x1 < 0 or y1 >= dis_height or y1 < 0:
        game_over = True
 
    x1 += newX
    y1 += newY
    dis.fill(white)
    pygame.draw.rect(dis, black, [x1, y1, snake_block, snake_block])
 
    pygame.display.update()
 
    clock.tick(snake_speed)
 
message("You lost",red)
pygame.display.update()
time.sleep(2)
```

5. Adding the Food
* [x] add food for the snake and create a message that says “Yummy!!”
* [x] include option to quit the game or play again when the player loses
```python snake_block = 10
snake_speed = 30
 
font_style = pygame.font.SysFont(None, 30)
 
 
def message(msg, color):
    mesg = font_style.render(msg, True, color)
    dis.blit(mesg, [dis_width/3, dis_height/3])
 
 
def gameLoop():  # creating a function
    game_over = False
    game_close = False
 
    x1 = dis_width / 2
    y1 = dis_height / 2
 
    newX = 0
    newY = 0
 
    foodx = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
    foody = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
 
    while not game_over:
 
        while game_close == True:
            dis.fill(white)
            message("You Lost! Press Q-Quit or C-Play Again", red)
            pygame.display.update()
 
            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:
                        gameLoop()
 
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    newX = -snake_block
                    newY = 0
                elif event.key == pygame.K_RIGHT:
                    newX = snake_block
                    newY = 0
                elif event.key == pygame.K_UP:
                    newY = -snake_block
                    newX = 0
                elif event.key == pygame.K_DOWN:
                    newY = snake_block
                    newX = 0
 
        if x1 >= dis_width or x1 < 0 or y1 >= dis_height or y1 < 0:
            game_close = True
 
        x1 += newX
        y1 += newY
        dis.fill(white)
        pygame.draw.rect(dis, blue, [foodx, foody, snake_block, snake_block])
        pygame.draw.rect(dis, black, [x1, y1, snake_block, snake_block])
        pygame.display.update()
 
        if x1 == foodx and y1 == foody:
            print("Yummy!!")
        clock.tick(snake_speed)
   ```
6. Increase Length of the Snake
* [x] use a list to create the snake length then increase the size of our sake when it eats the food 
* [x] the game is over if the snake hits its own body
```python
snake_List = []
    Length_of_snake = 1
 
    foodx = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
    foody = round(random.randrange(0, dis_height - snake_block) / 10.0) * 10.0
 
    while not game_over:
 
        while game_close == True:
            dis.fill(blue)
            message("You Lost! Press C-Play Again or Q-Quit", red)
 
            pygame.display.update()
 
            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:
                        gameLoop()
 
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    newX = -snake_block
                    newY = 0
                elif event.key == pygame.K_RIGHT:
                    newX = snake_block
                    newY = 0
                elif event.key == pygame.K_UP:
                    newY = -snake_block
                    newX = 0
                elif event.key == pygame.K_DOWN:
                    newY = snake_block
                    newX = 0
 
        if x1 >= dis_width or x1 < 0 or y1 >= dis_height or y1 < 0:
            game_close = True
        x1 += newX
        y1 += newY
        dis.fill(blue)
        pygame.draw.rect(dis, green, [foodx, foody, snake_block, snake_block])
        snake_Head = []
        snake_Head.append(x1)
        snake_Head.append(y1)
        snake_List.append(snake_Head)
        if len(snake_List) > Length_of_snake:
            del snake_List[0]
 
        for x in snake_List[:-1]:
            if x == snake_Head:
                game_close = True
 
        our_snake(snake_block, snake_List)
 ```
7. Display Score
```python
Your_score(Length_of_snake - 1)
```
## Output 

```python
import pygame
import time
import random
 
pygame.init()
 
white = (255, 255, 255)
yellow = (255, 255, 102)
black = (0, 0, 0)
red = (213, 50, 80)
green = (0, 255, 0)
blue = (50, 153, 213)
 
dis_width = 600
dis_height = 400
 
dis = pygame.display.set_mode((dis_width, dis_height))
 
clock = pygame.time.Clock()
 
snake_block = 10
snake_speed = 15
 
font_style = pygame.font.SysFont("bahnschrift", 25)
score_font = pygame.font.SysFont("comicsansms", 35)
 
 
def Your_score(score):
    value = score_font.render("Your Score: " + str(score), True, yellow)
    dis.blit(value, [0, 0])
 
 
 
def our_snake(snake_block, snake_list):
    for x in snake_list:
        pygame.draw.rect(dis, black, [x[0], x[1], snake_block, snake_block])
 
 
def message(msg, color):
    mesg = font_style.render(msg, True, color)
    dis.blit(mesg, [dis_width / 6, dis_height / 3])
 
 
def gameLoop():
    game_over = False
    game_close = False
 
    x1 = dis_width / 2
    y1 = dis_height / 2
 
    newX = 0
    newY = 0
 
    snake_List = []
    Length_of_snake = 1
 
    foodx = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
    foody = round(random.randrange(0, dis_height - snake_block) / 10.0) * 10.0
 
    while not game_over:
 
        while game_close == True:
            dis.fill(blue)
            message("You Lost! Press C-Play Again or Q-Quit", red)
            Your_score(Length_of_snake - 1)
            pygame.display.update()
 
            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:
                        gameLoop()
 
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    newX = -snake_block
                    newY = 0
                elif event.key == pygame.K_RIGHT:
                    newX = snake_block
                    newY = 0
                elif event.key == pygame.K_UP:
                    newY = -snake_block
                    newX = 0
                elif event.key == pygame.K_DOWN:
                    newY = snake_block
                    newX = 0
 
        if x1 >= dis_width or x1 < 0 or y1 >= dis_height or y1 < 0:
            game_close = True
        x1 += newX
        y1 += newY
        dis.fill(blue)
        pygame.draw.rect(dis, green, [foodx, foody, snake_block, snake_block])
        snake_Head = []
        snake_Head.append(x1)
        snake_Head.append(y1)
        snake_List.append(snake_Head)
        if len(snake_List) > Length_of_snake:
            del snake_List[0]
 
        for x in snake_List[:-1]:
            if x == snake_Head:
                game_close = True
 
        our_snake(snake_block, snake_List)
        Your_score(Length_of_snake - 1)
 
        pygame.display.update()
 
        if x1 == foodx and y1 == foody:
            foodx = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
            foody = round(random.randrange(0, dis_height - snake_block) / 10.0) * 10.0
            Length_of_snake += 1
 
        clock.tick(snake_speed)
 
    pygame.quit()
    quit()
 
 
gameLoop()
```
