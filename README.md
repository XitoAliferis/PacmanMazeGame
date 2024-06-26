# Pacman Maze Game Project

## Overview
This project is a Pacman-inspired maze game developed as part of a coursework project at the University of Miami. The game involves navigating a maze, avoiding enemies, and reaching the goal while collecting coins. The project showcases skills in C++ programming, file handling, graphics rendering, and game logic implementation.

## Features
- **Maze Generation**: The maze is read from a text file and rendered graphically.
- **Character Movement**: The player controls Pacman using keyboard inputs (W, A, S, D).
- **Enemies**: The game features two enemy robots with random movement patterns.
- **Goal**: The objective is to navigate Pacman to the coin while avoiding enemies.
- **Automatic and Manual Modes**: Players can switch between automatic and manual navigation.
- **Path Visualization**: Shows the path taken by Pacman after the game ends.
- **Replay Option**: Option to start a new game after the current game ends.

## Getting Started

### Prerequisites
- C++ Compiler (e.g., g++, clang++)
- Graphics library (e.g., SDL2, OpenGL)

### Installation
1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/pacman-maze-game.git
   ```
2. Navigate to the project directory:
   ```sh
   cd pacman-maze-game
   ```
3. Compile the code:
   ```sh
   g++ -o pacman_game main.cpp -lSDL2
   ```
4. Run the game:
   ```sh
   ./pacman_game
   ```

## Code Structure

### Main Components
- **Images**: Loaded images for Pacman, enemies, start, and goal.
- **Locations**: Structures to track positions in the maze.
- **Maze Handling**: Reading and drawing the maze from a text file.
- **Game Logic**: Player and enemy movement, collision detection, and game state management.

### Key Functions
- **read_file()**: Reads the maze layout from a file.
- **read_maze()**: Parses the maze file and initializes game objects.
- **draw_maze()**: Renders the maze on the screen.
- **yellowBrickRoad()**: Visualizes Pacman's path after the game ends.
- **game()**: Main game loop handling user input and game state updates.
- **new_game()**: Prompts the player to start a new game.
- **main()**: Initializes the game and enters the main game loop.

## Controls
- **W**: Move up
- **A**: Move left
- **S**: Move down
- **D**: Move right
- **N**: Switch to automatic mode
- **M**: Switch to manual mode
- **B**: Move back one step

## Example Maze File
```
++++++++++
+        +
+  # #   +
+  # $   +
+        +
++++++++++
```
- `+`: Start position
- `#`: Wall
- `$`: Goal

## Future Improvements
- **Enhanced Enemy AI**: Implement more sophisticated enemy movement algorithms.
- **Maze Variety**: Add different maze layouts and increase complexity.
- **Power-Ups**: Introduce power-ups to enhance gameplay.

## Acknowledgements
This project was developed by Xristopher Aliferis as part of the software engineering curriculum at the University of Miami. Special thanks to the faculty for their guidance and support.

## Contact
For any questions or suggestions, please contact me at:
- Email: xaliferi@uwo.ca
- LinkedIn: [Xristopher Aliferis](https://linkedin.com/in/xristopher-aliferis)
- GitHub: [XitoAliferis](https://github.com/XitoAliferis)

---

Feel free to explore, modify, and enhance the game. Contributions are welcome!
