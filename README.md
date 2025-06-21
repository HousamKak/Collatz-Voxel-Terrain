# Enhanced Collatz Voxel Terrain

An interactive 3D voxel world generated from the Collatz sequence, powered by Three.js and procedural noise. Explore infinite mathematical landscapes, hunt for hidden treasures, and uncover special "discoveries" as you traverse terrain shaped by one of mathematics' most curious sequences.

---

## 📖 Table of Contents

- [Overview](#overview)  
- [Features](#features)  
- [Screenshots](#screenshots)  
- [Getting Started](#getting-started)  
  - [Prerequisites](#prerequisites)  
  - [Installation](#installation)  
  - [Running Locally](#running-locally)  
- [Controls & UI](#controls--ui)  
- [Configuration & Customization](#configuration--customization)  
- [Project Structure](#project-structure)  
- [How It Works](#how-it-works)  
- [Future Improvements](#future-improvements)  
- [Contributing](#contributing)  
- [License](#license)  

---

## 🌐 Overview

This project transforms the Collatz sequence into a richly textured 3D voxel terrain. Each voxel's height and material are influenced by both multi-octave simplex noise and the values from a user-specified Collatz sequence "seed." Enhanced UI overlays, a minimap, and interactive features (treasures, discoveries, waypoints) turn mathematical exploration into a playful experience.

---

## ✨ Features

- **Procedural Terrain**  
  - Multi-octave Simplex noise for realistic hills and valleys  
  - Collatz sequence modulation for mathematically driven elevation changes  

- **Dynamic Materials**  
  - Five customizable texture packs (Classic, Realistic, Volcanic, Neon, Crystal)  
  - Procedural canvas-generated base maps and normal maps  

- **Performance Optimizations**  
  - Instanced meshes for large block groups  
  - Frustum-culled geometries with accurate bounding spheres  
  - ACES tone mapping, sRGB output, high-performance WebGL settings  

- **Interactive HUD & Controls**  
  - Live FPS, block count, mesh count, Collatz stats  
  - Pause menu for seed, scale, size, height adjustments  
  - In-game minimap with treasures, waypoints, and player marker  

- **Map Activities**  
  - 🎯 5 hidden treasures placed at Collatz "peaks"  
  - 🔍 3 special "discoveries" based on mathematical patterns  
  - 📍 Place and teleport to custom waypoints  

- **Utility**  
  - Screenshot export  
  - Fullscreen toggle  
  - Adjustable movement speed, mouse sensitivity, terrain animation  

---

## 📸 Screenshots

*(Replace with your own images or GitHub-hosted assets.)*

---

## 🚀 Getting Started

### Prerequisites

- A modern browser with WebGL support (Chrome, Firefox, Edge).  
- No build tools required—just open the HTML file or serve via a simple HTTP server.

### Installation

1. **Clone this repository** (or download the HTML file directly):

   ```bash
   git clone https://github.com/yourusername/collatz-voxel-terrain.git
   cd collatz-voxel-terrain
   ```

2. **(Optional)** If you'd like to host locally with live-reload:

   ```bash
   # Using Node.js's http-server
   npm install -g http-server
   http-server . -c-1
   ```

### Running Locally

* **Directly**:
  Simply open `index.html` in your browser.

* **Via HTTP server** (recommended for consistent behavior):

  ```bash
  http-server . -c-1
  # Then navigate to http://localhost:8080
  ```

---

## 🎮 Controls & UI

| Action                             | Key / UI Element          |
| ---------------------------------- | ------------------------- |
| Move Forward / Back / Left / Right | W / S / A / D             |
| Jump                               | Space                     |
| Run                                | Shift                     |
| Look Around                        | Mouse (after click)       |
| Pause / Settings Menu              | Esc                       |
| Toggle Minimap                     | M                         |
| Toggle Performance Overlay         | P                         |
| Cycle Texture Pack                 | T (or click in UI)        |
| Fullscreen                         | F (or button)             |
| Screenshot                         | UI "📸 Screenshot" button |
| Place Waypoint (Minimap)           | Click on map canvas       |
| Teleport to Waypoint               | "Go to Waypoint" button   |

Hover over sliders and buttons for tooltips in the pause menu.

---

## ⚙️ Configuration & Customization

All key parameters live in the `<script>` section of `index.html`:

```js
const CONFIG = {
  WORLD: {
    DEFAULT_SIZE: 64,
    MAX_HEIGHT: 50,
    INSTANCING_THRESHOLD: 50,
  },
  PLAYER: {
    BASE_SPEED: 100,
    RUN_MULTIPLIER: 2,
    JUMP_POWER: 12,
    MOUSE_SENSITIVITY: 0.003,
  },
  RENDERING: {
    FOV: 75,
    NEAR: 0.1,
    FAR: 1000,
  },
  MATERIALS: {
    ENABLE_TEXTURES: true,
    ENABLE_NORMAL_MAPS: true,
  }
};
```

* **Texture Packs**: Modify or add new packs in the `TEXTURE_PACKS` object.
* **Procedural Patterns**: Tweak functions like `addStonePattern` or `addGrassPattern`.
* **Collatz Modulation**: Control how much the sequence influences terrain in `generateHeightMap()`.

---

## 📂 Project Structure

```
.
├── index.html          # Main HTML & embedded CSS/JS
├── README.md           # (You are here)
└── assets/             # (Optional) External textures or icons
```

Everything lives in a single HTML file for ease of distribution; you can split CSS/JS into separate files if preferred.

---

## 🧠 How It Works

1. **Collatz Sequence**

   * `getCollatzSequence(seed)` builds the sequence and tracks its maximum value.

2. **Terrain Generation**

   * Two `SimplexNoise` instances provide base height variation.
   * The sequence is sampled modulo its max to modulate elevation.
   * Heights are normalized, then mapped to `[0,1]`.

3. **Voxel Mesh Creation**

   * Heights ⇒ integer block stacks per `(x,z)` column.
   * Blocks grouped by material type; large groups use `InstancedMesh`.
   * Shared `BoxGeometry` and per-material `MeshStandardMaterial` with canvas textures.

4. **Interactive Features**

   * UI overlays updated each frame in `gameLoop()`.
   * Minimap rendered to a `<canvas>` with treasures, waypoints, and player marker.

---

## 🔭 Future Improvements

* ✨ Add day/night cycle with dynamic lighting.
* 🗺️ Export/import custom Collatz seeds or terrain snapshots.
* ⛏️ Support custom block shapes or biomes.
* 🤖 Automated testing for generation correctness and performance benchmarks.

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch (`git checkout -b feat/awesome`)
3. Commit your changes
4. Open a pull request

Please keep changes focused and document new features in this README.

---

## 📄 License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for more information.