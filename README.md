import pygame

pygame.init()


window_size = (800, 600)
window = pygame.display.set_mode(window_size)
pygame.display.set_caption("Меню")

clock = pygame.time.Clock()
FPS = 60


filename = "settings.json"


difficulties = ["hard", "medium", "easy"]
current_difficulty = 0
max_index = 2


class Button:
    def __init__(self, x, y, width, height, color):
        self.rect = pygame.Rect(x, y, width, height)
        self.color = color

    def draw(self):
        pygame.draw.rect(window, self.color, self.rect)

    def is_clicked(self, event):
        return (
            event.type == pygame.MOUSEBUTTONDOWN
            and self.rect.collidepoint(event.pos)
        )



play_button = Button(300, 200, 200, 60, (0, 150, 0))
exit_button = Button(300, 300, 200, 60, (150, 0, 0))


while True:

    window.fill((30, 30, 30))


    font = pygame.font.SysFont(None, 36)
    text = font.render(difficulties[current_difficulty], True, (255, 255, 255))
    window.blit(text, (320, 120))

    for event in pygame.event.get():

        if event.type == pygame.QUIT:
            pygame.quit()
            quit()

        if play_button.is_clicked(event):
            print("Гра почалась")

        if exit_button.is_clicked(event):
            pygame.quit()
            quit()


        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                current_difficulty += 1

                if current_difficulty > max_index:
                    current_difficulty = 0

    play_button.draw()
    exit_button.draw()

    pygame.display.update()
    clock.tick(FPS)
