import pygame
import sys

# Khởi tạo Pygame
pygame.init()

# Thiết lập các tham số cho màn hình
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Minecraft-like Game")

# Màu sắc
WHITE = (255, 255, 255)
GREEN = (0, 255, 0)
BROWN = (139, 69, 19)

# Kích thước khối
BLOCK_SIZE = 40

# Lớp khối
class Block:
    def __init__(self, x, y, color):
        self.x = x
        self.y = y
        self.color = color

    def draw(self):
        pygame.draw.rect(screen, self.color, (self.x, self.y, BLOCK_SIZE, BLOCK_SIZE))

# Danh sách khối
blocks = []

# Vị trí người chơi
player_x = WIDTH // 2
player_y = HEIGHT // 2

# Vòng lặp chính
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        
        # Đặt khối
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                blocks.append(Block(player_x, player_y, BROWN))

    # Xử lý di chuyển người chơi
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        player_x -= 5
    if keys[pygame.K_RIGHT]:
        player_x += 5
    if keys[pygame.K_UP]:
        player_y -= 5
    if keys[pygame.K_DOWN]:
        player_y += 5

    # Làm mới màn hình
    screen.fill(WHITE)

    # Vẽ các khối
    for block in blocks:
        block.draw()

    # Vẽ người chơi
    pygame.draw.rect(screen, GREEN, (player_x, player_y, BLOCK_SIZE, BLOCK_SIZE))

    pygame.display.flip()
    pygame.time.Clock().tick(60)  # Giới hạn FPS
