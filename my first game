import pygame
from random import*

pygame.init() 

screen_width = 480 
screen_height = 640 
screen = pygame.display.set_mode((screen_width, screen_height))

pygame.display.set_caption("창식 게임") 

clock = pygame.time.Clock()

# 배경 로드
background = pygame.image.load("C:\\Users\\kcs91\\Desktop\\workspace\\python workspace\\nado coding\\pygame_basic\\background.png")

# 캐릭터 만들기
character = pygame.image.load("C:\\Users\\kcs91\\Desktop\\workspace\\python workspace\\nado coding\\pygame_basic\\character.png") 
character_size = character.get_rect().size
character_width = character_size[0]
character_height = character_size[1]
character_x_pos = screen_width / 2 -character_width / 2
character_y_pos = screen_height - character_height
character_to_x = 0
character_speed = 0.6

# 똥 만들기
enemy = pygame.image.load("C:\\Users\\kcs91\\Desktop\\workspace\\python workspace\\nado coding\\pygame_basic\\enemy.png") 
enemy_size = enemy.get_rect().size
enemy_width = enemy_size[0]
enemy_height = enemy_size[1]
enemy_x_pos = randint(0, screen_width - enemy_width)
enemy_y_pos = 0
enemy_speed = 0.6

game_font = pygame.font.Font(None, 40)

total_time = 10

start_ticks = pygame.time.get_ticks()


running = True 
while running:
    dt = clock.tick(30) # 게임화면의 초당 프레임수를 설정
    # 이벤트 처리 (키보드, 마우스 등)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:  
            running = False 

        # 캐릭터 이동 설정
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                character_to_x -= character_speed
            elif event.key == pygame.K_RIGHT:
                character_to_x += character_speed
        
        if event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT or event.key == pygame.K_RIGHT:
                character_to_x = 0

        # 똥 이동 설정
        if enemy_y_pos >= screen_height:
            enemy_y_pos = 0
            enemy_x_pos = randint(0, screen_width - enemy_width)
        
    # 캐릭터, 똥 위치 변화
    character_x_pos += character_to_x * dt
    enemy_y_pos += enemy_speed * dt

    # 화면 밖으로 못나가게
    if character_x_pos < 0 :
        character_x_pos = 0
    elif character_x_pos > screen_width - character_width:
        character_x_pos = screen_width - character_width

    # 충돌 설정
    character_rect = character.get_rect()
    character_rect.left = character_x_pos
    character_rect.top = character_y_pos

    enemy_rect = enemy.get_rect()
    enemy_rect.left = enemy_x_pos
    enemy_rect.top = enemy_y_pos

    if character_rect.colliderect(enemy_rect):
        print("충돌!")
        running = False

    # 시간 설정
    elapsed_time = (pygame.time.get_ticks() - start_ticks) /1000
    timer = game_font.render(str(int(total_time - elapsed_time)), True, (255, 255, 255))
           
    if total_time - elapsed_time <= 0:
        print("time out")
        running = False


# 화면에 출력
    screen.blit(background, (0,0))
    screen.blit(character, (character_x_pos, character_y_pos))
    screen.blit(enemy, (enemy_x_pos, enemy_y_pos)) 
    screen.blit(timer, (10, 10)) 
    pygame.display.update() 

# 딜레이
pygame.time.delay(2000)

pygame.quit()
