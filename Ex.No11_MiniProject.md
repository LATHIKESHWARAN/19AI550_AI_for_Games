# Ex.No: 11  Mini Project - AI battle Arena
### DATE:                                                                            
### REGISTER NUMBER : 212222230072
### AIM: 
To write a Python program using Pygame to simulate a game where a player character engages AI-controlled enemies with health, scoring, and respawn mechanics.
### Algorithm:
**1.Initialize the Game:**

  Initialize Pygame and set up the display with a specified window size.
  
  Load images for the player, enemies, and background, scaling them to fit the screen.
  
  Define colors and fonts for health bars and score display.
  
  Define Classes for Game Entities:

**2. Player Class:**
   
  Set initial position, health, and a health bar to display remaining health.

  Define movement functions with boundary checks to keep the player within screen limits.
  
  Implement a draw function to render the player and its health bar.
  
**3. Enemy Class:**
   
  Randomly position each enemy on the screen.

  Implement movement towards the player using basic tracking logic.
  
  Implement a draw function to render each enemy and its health bar.
  
**4. Game Logic and Main Loop:**

  Create instances of the player and multiple enemies.
  
  Start the main game loop, which runs while the player’s health is above zero:
  
  Handle Events: Check for quit events to close the game.
  
  Player Movement: Update player position based on keyboard input.
  
  Enemy Behavior: For each enemy:
  
  Move the enemy towards the player’s position.
  
  Check for collisions between the player and each enemy.
  
  Reduce player and enemy health upon collision.
  
  Remove and respawn the enemy if its health reaches zero, and increment the player’s score.
  
  Display Score and Health: Continuously display the player’s score and health.
  
**5. Game Over:**

  Display a “Game Over” screen showing the player’s final score.
  Close the game after a short delay.
### Program:
```
import pygame
import random

# Initialize Pygame
pygame.init()

# Set screen size
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("AI Battle Game")

# Load images
player_img = pygame.image.load("player.png").convert_alpha()  # Path to your player image
enemy_img = pygame.image.load("enemy.png").convert_alpha()    # Path to your enemy image
background_img = pygame.image.load("backgroun.jpeg").convert()  # Path to your background image

# Scale images to appropriate size
player_img = pygame.transform.scale(player_img, (50, 50))
enemy_img = pygame.transform.scale(enemy_img, (50, 50))
background_img = pygame.transform.scale(background_img, (WIDTH, HEIGHT))

# Set colors
RED = (255, 0, 0)
GREEN = (0, 255, 0)
WHITE = (255, 255, 255)

# Player class
class Player:
    def __init__(self):
        self.rect = player_img.get_rect(center=(WIDTH//2, HEIGHT//2))
        self.health = 100
        self.score = 0

    def move(self, dx, dy):
        self.rect.x += dx
        self.rect.y += dy
        # Keep player within screen bounds
        self.rect.x = max(0, min(self.rect.x, WIDTH - self.rect.width))
        self.rect.y = max(0, min(self.rect.y, HEIGHT - self.rect.height))

    def draw(self):
        screen.blit(player_img, self.rect)
        self.draw_health_bar()

    def draw_health_bar(self):
        pygame.draw.rect(screen, GREEN, (self.rect.x, self.rect.y - 3, self.health * 1.5, 5))

# Enemy class
class Enemy:
    def __init__(self):
        self.rect = enemy_img.get_rect(topleft=(random.randint(0, WIDTH-50), random.randint(0, HEIGHT-50)))
        self.health = 50

    def move_towards_player(self, player_rect):
        if self.rect.x < player_rect.x:
            self.rect.x += 1
        if self.rect.x > player_rect.x:
            self.rect.x -= 1
        if self.rect.y < player_rect.y:
            self.rect.y += 1
        if self.rect.y > player_rect.y:
            self.rect.y -= 1

    def draw(self):
        screen.blit(enemy_img, self.rect)
        self.draw_health_bar()

    def draw_health_bar(self):
        pygame.draw.rect(screen, RED, (self.rect.x, self.rect.y - 10, self.health, 5))

# Main game loop
def main():
    clock = pygame.time.Clock()
    player = Player()
    enemies = [Enemy() for _ in range(5)]  # Initialize enemies
    running = True
    font = pygame.font.Font(None, 36)

    while running:
        screen.blit(background_img, (0, 0))  # Draw background

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

        # Player movement
        keys = pygame.key.get_pressed()
        dx = (keys[pygame.K_RIGHT] - keys[pygame.K_LEFT]) * 5
        dy = (keys[pygame.K_DOWN] - keys[pygame.K_UP]) * 5
        player.move(dx, dy)

        # Update and draw player and enemies
        player.draw()
        for enemy in enemies[:]:  # Copy list to avoid mutation issues
            enemy.move_towards_player(player.rect)
            enemy.draw()

            # Check for collisions
            if player.rect.colliderect(enemy.rect):
                player.health -= 1  # Damage player
                enemy.health -= 5  # Damage enemy

            # Remove enemy if health is 0 and respawn
            if enemy.health <= 0:
                enemies.remove(enemy)
                player.score += 10  # Increase score
                enemies.append(Enemy())  # Respawn a new enemy

            # End game if player health is 0
            if player.health <= 0:
                running = False

        # Display player score
        score_text = font.render(f"Score: {player.score}", True, WHITE)
        screen.blit(score_text, (10, 10))

        # Refresh display
        pygame.display.flip()
        clock.tick(60)

    # Game Over Screen
    screen.fill((0, 0, 0))
    game_over_text = font.render("Game Over", True, WHITE)
    final_score_text = font.render(f"Final Score: {player.score}", True, WHITE)
    screen.blit(game_over_text, (WIDTH // 2 - game_over_text.get_width() // 2, HEIGHT // 2 - 50))
    screen.blit(final_score_text, (WIDTH // 2 - final_score_text.get_width() // 2, HEIGHT // 2 + 10))
    pygame.display.flip()
    pygame.time.wait(3000)
    pygame.quit()

if __name__ == "__main__":
    main()
```
### Output:
![Screenshot 2024-11-12 101949](https://github.com/user-attachments/assets/caf442ea-a238-4bb3-bfa9-d9d258b8c0c3)

![Screenshot 2024-11-12 102000](https://github.com/user-attachments/assets/4254762b-4de4-401a-aebc-21437ad5e7bb)



### Result:
Thus,The game was successfully implemented using Python and Pygame, providing an interactive experience with AI-based enemy pursuit, player health, scoring, and continuous gameplay.
