import pygame
import random

# Initialisierung von Pygame
pygame.init()

# Konstanten für Bildschirmgröße und Farben
SCREEN_WIDTH, SCREEN_HEIGHT = 400, 600
WHITE = (255, 255, 255)

# Initialisierung des Bildschirms
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption('Tetris Clone')

# Definition der Tetrominos (I, J, L, O, S, T, Z)
tetrominos = [
    [[1, 1, 1, 1]],
    [[1, 1, 1],
     [0, 0, 1]],
    [[1, 1, 1],
     [1, 0, 0]],
    [[1, 1],
     [1, 1]],
    [[0, 1, 1],
     [1, 1, 0]],
    [[1, 1, 1],
     [0, 1, 0]],
    [[1, 1, 0],
     [0, 1, 1]]
]

# Klasse für Tetromino
class Tetromino:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.shape = random.choice(tetrominos)
        self.color = random.choice([(255, 0, 0), (0, 255, 0), (0, 0, 255)])

    def draw(self):
        for i in range(len(self.shape)):
            for j in range(len(self.shape[i])):
                if self.shape[i][j]:
                    pygame.draw.rect(screen, self.color, (self.x + j * 30, self.y + i * 30, 30, 30))

# Schleife für das Spiel
clock = pygame.time.Clock()
running = True

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Spielfeld zeichnen
    screen.fill(WHITE)
    
    # Tetromino zeichnen und bewegen
    tetromino = Tetromino(SCREEN_WIDTH // 2 - 15, SCREEN_HEIGHT // 2 - 15)
    tetromino.draw()
    
    # Spielfeld aktualisieren
    pygame.display.flip()
    
    # Bildschirm aktualisieren
    clock.tick(30)

# Pygame beenden
