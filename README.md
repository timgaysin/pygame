# coding: utf8
import pygame
import random

# задааем размер окна, создаем окно размера size
size = [400, 400]
window = pygame.display.set_mode(size)
# задаем имя - в кавычках, т.к. текст - это строка
pygame.display.set_caption('My second file')

screen = pygame.Surface(size)


class Sprite:
    def __init__(self, xpos, ypos, filename):
        self.x = xpos
        self.y = ypos
        self.bitmap = pygame.image.load(filename)

    def render(self):
        screen.blit(self.bitmap, (self.x, self.y))


def Intersect(s1_x, s2_x, s1_y, s2_y):
    if ((s1_x > s2_x - 40) and (s1_x < s2_x + 40) and (s1_y > s2_y - 40) and (s1_y < s2_y + 40)):
        return 1
    else:
        return 0

# создание персонажей
# герой
hero = Sprite(200, 350, 'mouse.jpg')
# переменные-"переключатели" движения для героя
hero.right = True
hero.up = True
hero.down = False
# враг
enemy = Sprite(200, 10, 'cat.jpg')
# переменные-"переключатели" движения для врага
enemy.right = True
enemy.up = True

pygame.key.set_repeat(1,1)

running = True
while running:
    # обработка событий
    for e in pygame.event.get():
        if e.type == pygame.QUIT:
            running = False
    for e in pygame.event.get():
        if e.type==pygame.KEYDOWN:
            if e.key==pygame.K_LEFT:
                if hero.x>=0:
                    hero.x-=5

    for e in pygame.event.get():
        if e.type==pygame.KEYDOWN:
            if e.key==pygame.K_RIGHT:
                if hero.x>=0:
                    hero.x+=5









    if hero.up==True:
        hero.y -= 2
        if hero.y <= 0:
            hero.up=False
    if hero.up==False:
        hero.y += 2
        if hero.y >= 368:
            hero.up=True



    if enemy.up==True:
        enemy.y-=2
        if enemy.y<=0:
            enemy.up=False
    if enemy.up==False:
        enemy.y += 2
        if enemy.y >= 370:
            enemy.up=True






    # задайте фоновый цвет
    screen.fill([23, 198, 93])

    # движение персонажей - аналогично тому,
    # что делали с квадратом, но теперь по вертикали

    # enemy.x = random.randint(0, 400)
    # enemy.y = random.randint(0, 400)

    # столкновение персонажей
    if Intersect(hero.x, enemy.x, hero.y, enemy.y):
        hero.up = False
        enemy.up = True

    # отображение персонажей
    hero.render()
    enemy.render()

    # отображение окна
    window.blit(screen, [0, 0])
    pygame.display.flip()
    pygame.time.delay(5)

pygame.quit()
