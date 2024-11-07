import random
import webbrowser

# Configurations for the game
GRID_SIZE = 10       # 10x10 grid
NUM_MINES = 15       # Number of mines

class Minesweeper:
    def __init__(self):
        self.grid = [[' ' for _ in range(GRID_SIZE)] for _ in range(GRID_SIZE)]
        self.mines = set()
        self.flags = set()
        self.game_over = False
        self.create_mines()
        self.revealed = set()

    def create_mines(self):
        while len(self.mines) < NUM_MINES:
            x = random.randint(0, GRID_SIZE - 1)
            y = random.randint(0, GRID_SIZE - 1)
            if (x, y) not in self.mines:
                self.mines.add((x, y))

    def display_grid(self):
        for i in range(GRID_SIZE):
            for j in range(GRID_SIZE):
                if (i, j) in self.revealed:
                    print(self.count_adjacent_mines(i, j), end=' ')
                elif (i, j) in self.flags:
                    print('F', end=' ')
                else:
                    print('X', end=' ')
            print()

    def count_adjacent_mines(self, x, y):
        # Count mines around a given cell
        adjacent_mines = 0
        for nx, ny in self.get_neighbors(x, y):
            if (nx, ny) in self.mines:
                adjacent_mines += 1
        return adjacent_mines

    def get_neighbors(self, x, y):
        # Get all valid neighboring cells (excluding the current cell)
        neighbors = []
        for dx in (-1, 0, 1):
            for dy in (-1, 0, 1):
                nx, ny = x + dx, y + dy
                if 0 <= nx < GRID_SIZE and 0 <= ny < GRID_SIZE and (nx, ny) != (x, y):
                    neighbors.append((nx, ny))
        return neighbors

    def reveal(self, x, y):
        if self.game_over or (x, y) in self.revealed:
            return

        if (x, y) == (GRID_SIZE - 1, GRID_SIZE - 1):
            webbrowser.open("https://www.example.com")  # Redirect to website
            self.game_over = True
            print("You clicked the bottom-right corner, redirecting...")
            return

        if (x, y) in self.mines:
            self.game_over = True
            print(f"Game Over! You hit a mine at ({x}, {y}).")
            return

        # Reveal the tile
        self.revealed.add((x, y))

        # If no adjacent mines, reveal neighbors recursively
        if self.count_adjacent_mines(x, y) == 0:
            for nx, ny in self.get_neighbors(x, y):
                self.reveal(nx, ny)

    def toggle_flag(self, x, y):
        if (x, y) in self.flags:
            self.flags.remove((x, y))
        else:
            self.flags.add((x, y))

    def play(self):
        while not self.game_over:
            self.display_grid()
            action = input("Enter action (reveal [x y] or flag [x y]): ").split()

            if len(action) != 3:
                print("Invalid input! Please follow the format: [action] [x] [y].")
                continue

            cmd, x, y = action[0], int(action[1]), int(action[2])

            if cmd == 'reveal':
                self.reveal(x, y)
            elif cmd == 'flag':
                self.toggle_flag(x, y)
            else:
                print("Invalid action! Please use 'reveal' or 'flag'.")

            if self.game_over:
                self.display_grid()
                print("Game Over!")


if __name__ == "__main__":
    game = Minesweeper()
    game.play()
