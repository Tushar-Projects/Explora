Explora: An Audio-Tactile Cave Exploration Game

"Play the Live Prototype on GitHub Pages" (https://tushar-projects.github.io/Explora/)

Explora is a browser-based prototype of an audio-tactile cave exploration game designed from the ground up for blind and visually impaired children.

Most accessible games start as visual experiences, with screen-reader support or audio cues added afterward. Explora takes a different approach. It treats spatial sound, tactile pattern recognition, and memory as the primary gameplay mechanics.

The visual interface serves as a 3D hardware simulator for sighted developers, educators, and observers, while the core experience is designed to be playable entirely without sight.

---

Live Demo

You can experience the complete prototype directly in your browser without installing anything.

- Live URL: https://tushar-projects.github.io/Explora/

«Audio tip: Modern browsers block audio playback and speech synthesis until the user interacts with the page. When the website loads, press any key or click the welcome overlay to initialize the Web Audio and Speech engines.»

---

Why We Built This

Refreshable tactile displays open up exciting possibilities for non-visual gaming. However, hardware constraints such as limited pin resolution and physical actuator refresh delays require a fundamentally different approach to interaction design.

Explora explores how these physical constraints can become part of an engaging gaming experience.

By combining a low-resolution tactile grid simulation with procedural audio and concise voice guidance, players can experience the atmosphere of exploring underground caverns, listening to echoes, and discovering hidden relics using sound and tactile information.

---

Core Gameplay and Mechanics

1. Echo Pulse System

Players navigate a grid-based cavern one step at a time. Since a tactile surface only reveals information that has been physically touched or scanned, players can emit an Echo Pulse to detect nearby tiles within a limited radius.

The echo returns spatial audio cues corresponding to nearby objects:

- Treasures: A bright, metallic harmonic chime that rises in pitch and clarity as the player gets closer.
- Cave Walls: A hollow, low-frequency knock panned in the direction of the obstacle.
- Cave Beetles (Hazards): A rhythmic, pulsing heartbeat that speeds up when a creature is nearby.
- Cavern Exit: A warm, resonant chord that signals the exit once all treasures have been collected.

2. Simulated Refreshable Tactile Display

Built with Three.js, the centerpiece of Explora simulates a physical, dark-anodized tactile pin matrix supporting grid sizes ranging from 6×6 to 8×8 cells.

Distinct tactile geometries:

- Walls: Solid raised structures with a 3×3 ridge pattern.
- Treasures: Raised octagonal gems surrounded by a tactile ring.
- Hazards: Irregular, spiky pin clusters.
- Player: A distinctive central beacon represented by a pulsing cylinder.

Hardware latency simulation:

Physical tactile pins require time to rise and fall. Explora simulates configurable actuation delays:

- Movement: approximately 150–250 ms.
- Echo scans: approximately 350 ms.
- Full board transitions: approximately 650 ms.

These transitions are accompanied by subtle mechanical pin-click audio.

Tactile Memory vs. Observer Mode:

By default, the display operates in Tactile Memory Mode, raising pins only for tiles the player has physically visited or revealed through an echo pulse.

Sighted testers can switch to Observer Mode to inspect the entire generated cavern.

3. Procedural Audio and Coordinated Speech

Explora uses no external MP3 or WAV sound assets.

Every sound effect, including footsteps, wall collisions, sonar sweeps, pin clicks, and achievement fanfares, is synthesized in real time using the Web Audio API.

Audio features include:

- Stereo panning.
- Frequency modulation.
- Procedural sound generation.
- Distinct audio signatures for different gameplay events.
- Coordinated speech and sound playback.

Spoken guidance uses the browser's SpeechSynthesis API. Voice prompts are coordinated with audio feedback so that speech does not unnecessarily overlap with important sound cues.

4. Guaranteed Solvable Procedural Caves

Every level is generated dynamically and verified using a Breadth-First Search (BFS) pathfinding algorithm.

The generator verifies that every treasure and the cavern exit are reachable from the starting position before the level loads.

This prevents frustrating dead ends and ensures that generated levels remain playable.

---

Controls and Keyboard Shortcuts

Explora is designed to support keyboard-only gameplay and screen-reader-friendly interaction.

Key / Input| Action
Arrow Keys or W, A, S, D| Move one grid cell North, West, South, or East
Spacebar or E| Emit an Echo Pulse to scan surrounding tiles
I or L| Speak current coordinates, remaining treasures, and exit status
R| Repeat the last spoken instruction or audio cue
H| Hear a summary of controls
M| Toggle between Tactile Memory Mode and Sighted Observer Mode
Escape| Pause the game or return to the main menu

---

Progression and Game Modes

Interactive Self-Voicing Tutorial

A guided, five-step onboarding cave teaches players:

1. Directional movement.
2. Wall collisions.
3. Echo scanning.
4. Treasure collection.
5. Finding the exit.

The tutorial is designed to teach gameplay without requiring a sighted adult to explain the rules.

Five Campaign Caverns

The campaign introduces progressively challenging environments:

- Starts with a relatively simple 6×6 cavern.
- Expands to 8×8 layouts.
- Introduces tighter echo cooldowns.
- Adds multiple relics.
- Introduces patrolling Cave Beetles.

Procedural Endless Mode

Unlocks after campaign progression, allowing players to explore continuously generated caverns with randomized layouts and objectives.

Persistent Progress and Achievements

Explora automatically saves:

- Unlocked levels.
- Lifetime gameplay statistics.
- Steps taken.
- Echoes used.
- Relics discovered.
- Audio and tactile preferences.

Progress and settings are stored locally using "localStorage".

---

Tech Stack

Technology| Purpose
HTML5| Application structure and semantic markup
CSS3| Styling, responsive layouts, and visual presentation
Tailwind CSS| Utility-based styling
Vanilla JavaScript (ES6+)| Game logic and application functionality
Three.js (r128)| 3D rendering, tactile pin geometry, lighting, and animations
Web Audio API| Procedural sound synthesis and stereo spatialization
Web Speech API| Native browser text-to-speech
ARIA| Screen-reader accessibility and semantic interaction
LocalStorage| Persistent game progress and settings

---

Getting Started

Option 1: Play Online

Visit the hosted prototype:

https://tushar-projects.github.io/Explora/

Option 2: Run Locally

Explora does not require a Node.js build pipeline or package installation.

1. Clone the repository

git clone https://github.com/tushar-projects/Explora.git
cd Explora

2. Start a local development server

Using Python:

python -m http.server 8000

Using Node.js:

npx serve .

Alternatively, use the Live Server extension in Visual Studio Code.

3. Open the application

Navigate to:

http://localhost:8000

You can also open "index.html" directly in a browser if the project supports direct file access.

---

Code Architecture

The codebase is organized into modular components with distinct responsibilities.

Component| Responsibility
"CellTypes" & "GameConfig"| Centralized constants, level definitions, and achievement criteria
"SaveManager"| Reading, writing, and resetting player progress and accessibility settings
"AudioManager"| Web Audio API context, gain nodes, stereo panning, and procedural sound generation
"SpeechManager"| Speech synthesis, voice queue management, and live audio transcript updates
"Pathfinding" & "CaveGenerator"| Procedural grid generation, entity placement, and BFS solvability verification
"TactileDisplay3D"| Three.js scene, camera, lighting, 3D cell meshes, and hardware refresh simulation
"GameEngine"| Movement, echo scanning, creature AI, tutorial transitions, and UI coordination

The modular structure separates gameplay logic, rendering, audio processing, accessibility, and persistence to support easier maintenance and future extensions.

---

License

Explora is open-source software released under the MIT License.

Feel free to fork, modify, and adapt the project to explore new possibilities in accessible audio-tactile gaming.
