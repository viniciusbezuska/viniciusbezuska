import sys
import random
import pygame

# inicia o pygame
pygame. init()


#define a janela
largura, altura = 640, 480
tela1 = pygame. display.set_mode((largura, altura))
pygame.display.set_caption("movimento quadrado e maçã")

#defina as propriedades do quadrado
quadrado_tamanho = 40
quadrado_x, quadrado_y = largura // 2, altura // 2
velocidade = 5

maçã_tamanho = 40
maçã_x, maçã_y = largura - 60, altura - 60

def teletransportar_maçã():
    global maçã_x, maçã_y
    maçã_x = random.randint(0, largura - maçã_tamanho)
    maçã_y = random.randint(0, altura - maçã_tamanho)
#define a cor
cor_quadrado = (0, 128, 255)
cor_maçã = (255, 0, 0)
cor_fundo = (255, 255, 255)

#loop principal
while True:
    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
    teclas = pygame.key.get_pressed()
    if teclas[pygame.K_w]: #move para cima
        quadrado_y -= velocidade
    if teclas[pygame.K_s]: #move para a direita
        quadrado_y += velocidade
    if teclas[pygame.K_a]: #move para baixo
        quadrado_x -= velocidade
    if teclas[pygame.K_d]: #move para a esquerda
        quadrado_x += velocidade
    tela1.fill(cor_fundo)
    pygame.draw.rect(tela1, cor_quadrado, (quadrado_x, quadrado_y, quadrado_tamanho, quadrado_tamanho))
    pygame.draw.rect(tela1, cor_maçã, (maçã_x, maçã_y, maçã_tamanho, maçã_tamanho))
    #atualiza a tela
    pygame.display.flip()
    pygame.time.Clock().tick(30) # controla a taxa de atualização do jogo
