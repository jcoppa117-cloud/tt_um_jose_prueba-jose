## How it works

This design implements a classic **Snake Game** rendered over a standard VGA interface (640x480 at 60Hz) using a TinyVGA PMOD. 

- **Gameplay Area:** A 32x24 grid where each cell measures 16x16 pixels, centered on the VGA display.
- **Dynamic Speed Scaling:** As the snake eats food items and the score increases, the internal speed threshold decreases, making the snake move progressively faster and more challenging.
- **Collision Detection:** The game detects both boundary collisions (hitting the outer walls) and self-collision (if the snake's head runs into any segment of its own body), triggering a Game Over state.
- **Visual Score Bar:** A status bar at the top of the screen dynamically fills up horizontally based on the amount of food consumed.
- **Randomized Food Generation:** Utilizes a Linear Feedback Shift Register (LFSR) to generate pseudo-random coordinates for placing food inside the grid.
- **Input Control:** Interfaces with a Gamepad PMOD via `ui_in` (`ui_in[6]` data, `ui_in[5]` clock, `ui_in[4]` latch) to read directional inputs from the D-Pad and the **Start** button to restart after a game over.

## How to test

1. **Hardware Setup:** 
   - Connect a TinyVGA compatible PMOD to the design outputs (`uo_out`) to display the game on a VGA monitor.
   - Connect a Gamepad PMOD to the dedicated inputs (`ui_in[6:4]`).
2. **Operation:**
   - Power up the board and release reset (`rst_n` high).
   - Use the D-Pad on the gamepad to steer the green snake.
   - Guide the snake to eat the red food items to grow longer, increase your score, and make the game faster.
   - Avoid crashing into the screen borders or your own tail.
   - If a Game Over occurs, press the **Start** button on the gamepad to reset and play again.

## External hardware

- **TinyVGA PMOD:** Connected to `uo_out` for VGA video output to a monitor.
- **Gamepad PMOD (NES-style or compatible):** Connected to `ui_in[6:4]` (`pmod_data`, `pmod_clk`, `pmod_latch`) for player controls.
