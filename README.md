import pygame
import random

# Initialize pygame
pygame.init()

# Screen dimensions
WIDTH = 800
HEIGHT = 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))

# define the colours
BLACK = (0, 0, 0)
ORANGE = (255, 165, 0)
DARK_ORANGE = (255, 140, 0)
WHITE = (255, 255, 255)
DARK_BLUE = (25, 25, 112)
GREY = (169, 169, 169)
BROWN = (139, 69, 19)
YELLOW = (255, 255, 102)
BLUE_HUE = 112
PAVEMENT_GREY = (145, 145, 145)
GREEN = (6, 64, 43)

# Moon properties
moon_x = 100
moon_y = 320

# Sun properties
sun_x = 0
sun_y = 340
sun_rise = False

# Frame rate
clock = pygame.time.Clock()
FPS = 30
# count
count = 0
# Star properties
num_stars = 50

star_x = []
star_y = []

# generate x and y coordinates for each star
for i in range (0, num_stars):
    star_x.append(random.randint(0, WIDTH))
    star_y.append(random.randint(0, HEIGHT // 2))

sky_change = False
    
# Main game loop
while True:
  for event in pygame.event.get():
      if event.type == pygame.QUIT:
         pygame.quit()

  # Sky change conditions
  if moon_x >= WIDTH / 2:
      sky_change = True

  # Sky change conditions
  if sky_change and BLUE_HUE < 255:
      # colour cannot be greater than 255
      BLUE_HUE += 1
  
  # Draw the sky
  screen.fill((25, 25, BLUE_HUE))
  if sky_change == True and num_stars > 0:

  # Draw the stars
      # if sky changes, start drawing less stars
      num_stars -= 1
  for i in range (0, num_stars):
      pygame.draw.circle(screen, YELLOW, (star_x[i], star_y[i]), 2)

  # Moon
  moon_x += 2
  # when moon reaches middle of the screen we want to increase y
  if moon_x >= WIDTH / 2 + 20:
      moon_y += 2
  elif moon_x <= WIDTH / 2 - 20:
      moon_y -= 2

  # draw the moon
  pygame.draw.circle(screen, WHITE, (moon_x, moon_y), 40)

  # sun movement
  if moon_x >= 500:
      # sun rises if the moon reaches 500
      sun_rise = True   


  if sun_rise:
      # determine the new coordinates of the sun
      sun_x += 2
      if sun_x >= WIDTH / 2 + 20:
          sun_y += 2
      elif sun_x <= WIDTH / 2 - 20:
          sun_y -= 2
      # draw the sun
      pygame.draw.circle(screen, YELLOW, (sun_x, sun_y), 50)

    
    
  # Turning off the lamp
  if not sun_rise:
      # Lamp light
      pygame.draw.ellipse(screen, YELLOW, (220, 425, 20, 20))
  if sun_rise:
      # Turned off lamp light
      pygame.draw.ellipse(screen, GREY, (220, 425, 20, 20))
  # Lamp head
  pygame.draw.rect(screen, PAVEMENT_GREY, (220, 415, 20, 20))
  
  # Lamp
  pygame.draw.rect(screen, PAVEMENT_GREY, (200, 425, 20, 100))
  
  # House
  pygame.draw.rect(screen, GREY, (300, 350, 200, 150))  # House body
  pygame.draw.polygon(screen, BLACK, [(300, 350), (400, 250), (500, 350)])  # Roof

  # Windows on house
  pygame.draw.rect(screen, BLACK, (320, 380, 40, 40))
  pygame.draw.rect(screen, BLACK, (440, 380, 40, 40))
      
  # Door
  pygame.draw.rect(screen, BROWN, (380, 430, 40, 70))

  # Pavement
  pygame.draw.rect(screen, PAVEMENT_GREY, (0, 500, 800, 80))

  # Grass
  pygame.draw.rect(screen, GREEN, (0, 575, 800, 30))

  # Pumpkin made of ellipses
  pygame.draw.ellipse(screen, DARK_ORANGE, (360, 500, 60, 40))  # Pumpkin body
  pygame.draw.ellipse(screen, ORANGE, (370, 505, 40, 30))       # Inner pumpkin part
  pygame.draw.rect(screen, BROWN, (385, 495, 10, 10))           # Pumpkin stem
          
  # Update display
  pygame.display.flip()
  # frame rate
  clock.tick(FPS)
