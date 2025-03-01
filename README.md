# RockPaperScissors: WebGPU Rock-Paper-Scissors Simulation

## Overview

This is an interactive Rock-Paper-Scissors (RPS) simulation that uses **WebGPU** in the browser to compute the movement and evolution of hundreds of sprites. Each sprite represents **Rock**, **Paper**, or **Scissors**. The physics includes acceleration, bouncy walls, and a CPU-side collision system to handle “conversions.” For example, if **Rock** collides with **Scissors**, the Scissors becomes Rock.

## Features

* **Acceleration & speed limit**: Sprites accelerate toward prey (the type they can beat) and away from predators (the type that beats them). Their maximum velocity is capped.
* **Bouncy walls**: Sprites bounce back if they hit the canvas boundary.
* **Collision conversions**: If two different types collide, the losing type is converted into the winner.
* **Trails**: Optional toggle for partial transparency each frame (making the sprites leave motion trails).
* **Single-type detection**: If only one type remains, a 5-second timer starts. After that period, if there is still only one type left, the simulation resets.

## Usage

1. **Open** `<span>RPS.html</span>` in a browser that supports **WebGPU** (currently behind a flag in some browsers).
2. **Settings**:
   * **Items per Type**: How many sprites of each type to start with.
   * **Acceleration**: How quickly sprites speed up when chasing or fleeing.
   * **Max Speed**: Speed limit.
   * **Use Trails?**: Toggles whether sprites leave a fading trail.
   * Press **Apply** to restart the simulation with the new settings.
3. The scoreboard (top-left) tracks how many of each type remain.
4. If you see a message in the console saying “WebGPU is not supported,” it means your browser doesn’t have it enabled.

## How It Works

1. **Compute shader** (WGSL) runs each frame to update each sprite’s velocity and position in parallel.
2. **CPU-based collision**: The script downloads the updated sprite buffer each frame, checks collisions, and modifies sprite “types” accordingly.
3. **Rendering**: A simple 2D canvas draws the emoji at each sprite’s position.
4. **Single-type check**: Once only one type is left, the simulation will automatically reset after 5 seconds.

## Requirements

* **WebGPU-enabled browser** (Chrome Canary or another browser that supports WebGPU).
* A **GPU** that supports the required shader model.

## Troubleshooting

* If you get `<span>Uncaught SyntaxError: Invalid or unexpected token</span>` errors, ensure your file is saved in UTF-8 encoding. The emojis might cause issues otherwise.
* If **WebGPU** is not recognized, check your browser flags or try another browser.

## License

MIT License
