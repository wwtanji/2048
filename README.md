# 2048 — Vanilla JavaScript Game

This project is a custom implementation of the 2048 puzzle game written in pure HTML, CSS, and JavaScript, without any third-party libraries or frameworks. The game logic, rendering, animations, and input handling are all created manually, providing full control over every aspect of the game.

---

## Project Structure

- `index.html` — Contains the root structure and game container.
- `style.css` — All layout, animation, and responsive styling.
- `script.js` — Main script to initialize the game and handle input.
- `grid.js` — Class that generates the grid and manages cell logic.
- `cell.js` — Class representing individual cells on the board.
- `tile.js` — Class for managing tile rendering, animation, and merging.

---

## Game Mechanics

1. **Grid Initialization**  
   The game starts with a 4x4 grid containing 16 empty cells. Each cell is created dynamically via JavaScript and positioned using CSS Grid.

2. **Tile Spawning**  
   A tile with the value 2 or 4 appears in a random empty cell. Two tiles are generated when the game starts.

3. **Tile Movement**  
   Tiles are moved via arrow key input (Up, Down, Left, Right). Movement is handled by grouping cells by rows or columns, iterating through them, and applying movement logic.

4. **Merging Logic**  
   Tiles with the same value that collide are merged into a new tile with a doubled value. Merging only happens once per move per tile.

5. **Animations**  
   - Movement and appearance animations are implemented using CSS transitions.
   - Promises are used to synchronize logic with animation completion using `waitForTransitionEnd`.

6. **Game Over Check**  
   If no valid moves remain, a message is displayed indicating that the game is over.

---

## Key Features Implemented

- Adaptive layout using `vmin` units and CSS variables.
- Modular class-based architecture:
  - `Grid` handles structure and grouping.
  - `Cell` handles tile linking and availability.
  - `Tile` manages value, DOM updates, and transitions.
- Tile merging is handled via a queue to prevent double merges.
- No new tiles spawn if no actual movement occurred.
- Smooth, well-synchronized animations between movement and merging.

---

## Controls

| Key         | Action             |
|-------------|--------------------|
| Arrow Up    | Move tiles up      |
| Arrow Down  | Move tiles down    |
| Arrow Left  | Move tiles left    |
| Arrow Right | Move tiles right   |

After each move (if it resulted in changes), a new tile is generated.

---

## Input & Event Handling

- Input is handled via `keydown` events.
- Only one event listener is active at a time (`once: true`) to ensure atomic moves.
- After each valid input, a new tile is spawned only if movement occurred.

---

## Animation Handling

- Tiles animate via CSS `transition` and `animation` properties.
- Movement animations are awaited using a `Promise` returned by `waitForTransitionEnd`.
- Merging occurs only after all movement animations complete.

---

## Logic Flow

```text
handleInput(event)
│
├─> CanMoveDirection? (Up/Down/Left/Right)
│   └─ No → Skip movement, re-enable input
│
├─> await SlideTiles (grouped cells)
│   └─ Handles movement and tracks merge candidates
│
├─> await mergeTiles()
│   └─ Combines tiles, removes DOM elements, updates value
│
├─> spawn new tile if move occurred
│
└─> check Game Over
    └─ if no valid moves remain → show "Try again"
```

---

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/wwtanji/2048
   cd 2048
   ```

2. Open `index.html` in any modern browser.

No build tools or servers are required.


---

##  Author

Developed by [wwtanji](https://github.com/wwtanji)  
Inspired by the original [2048](https://github.com/gabrielecirulli/2048) by Gabriele Cirulli
