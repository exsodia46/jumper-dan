import pygame
pygame.init()
screen = pygame.display.set_mode((800, 600))
pygame.display.set_caption('Side-Scrolling Game')
clock = pygame.time.Clock()
isOnGround = False

player = [100, 440, 0, 0] #player place
isOnGround = False
offset = 0
platforms =[(500, 400), (700, 300)]

for i in range(len(platforms)):
    if player[0]+50>platforms[i][0]+offset and player[0]<platforms[i][0]+100+offset and player[1]+50>platforms[i][1] and player[1]+50:
        isOnGround = True
        player[1]=platforms[i][1]-50
        payer[3] = 0

def move_player():
      global isOnGround
      global offset
      #jumper thingopoper
      if isOnGround == True and keys [pygame.K_UP]:
          player[3] = -15 #HIM jump
          isOnGround = False
        
      if keys[pygame.K_LEFT]:
          #player[2] =- 5
          if offset > 260 and player[0]>0:
              player[2] = -5
              
              
          elif player[0]>400 and offset < -1500:
              player[2] = -5
         
              
          elif player[0]>0:
              offset += 5
              player[2] = 0
              
          else:
              player[2]=0
              
      elif keys[pygame.K_RIGHT]:
          if offset < -1500 and player[0]<400:
             player[2] = 5
             
          elif offset >260 and player[0]<400:
              player[2] = 5
      
          elif player[0]<750:
              offset -= 5
          
      else:
          player[2] = 0
        
      if isOnGround == False:
          player[3]+=1
      else:
          player[3] = 0
          
      player[0]+=player[2]
      player[1]+=player[3]
      if player[1] >= 450:
          isOnGround = True
      else:
          isOnGround = False
      
def draw_clouds():
    for x in range(100, 2000, 300):
        for i in range(3):
            pygame.draw.circle(screen, (35, 148, 45), (x + offset, 100), 40)
            pygame.draw.circle(screen, (35, 148, 45), (x - 47 + offset, 125), 40)
            pygame.draw.circle(screen, (35, 148, 45), (x + 57 + offset, 125), 40)
        pygame.draw.rect(screen, (35, 148, 45), (x - 50 + offset, 100, 100, 65))
       
       
      
def draw_tree():
    for x in range(100, 2000, 300):
        for i in range(3):
            pygame.draw.rect(screen, (149, 159, 191), (x + offset, 310, 40, 205)) #branch
            pygame.draw.circle(screen, (203, 209, 17), (x +20+offset, 220), 40)#leaves
            pygame.draw.circle(screen, (203, 209, 17), (x + 90 + offset, 315), 40)#leaves
            pygame.draw.circle(screen, (203, 209, 17), (x -20 + offset, 325), 40)#leaves
            pygame.draw.circle(screen, (0, 0, 0), (x+30 + offset, 279), 40)#leaves
        
        
def draw_platforms():
    for i in range(len(platforms)):
        pygame.draw.rect(screen, (150, 10, 10), (platforms[i][0] + offset, platforms[i][1], 100, 30))
        

running = True
while running: #main game loop+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
    clock.tick(60)
    #input section-----------------------------------------------------------
    for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
               
    keys = pygame.key.get_pressed()
    #physics section+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
    move_player()
    #render section++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
    screen.fill((43, 23, 61)) #sky blue background
    draw_clouds() #function call
    draw_tree()
    draw_platforms()
    pygame.draw.rect(screen, (74, 62, 7), (0, 500,1000, 505)) #grass
    pygame.draw.rect(screen, (105, 125, 7), ((player[0], player[1]), (50, 50))) #HIM
    pygame.display.flip()
   
pygame.quit()  
