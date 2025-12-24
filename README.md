# CV_to_StreetFighter: Robotics Edition 🤖🥊

**Fight the Future. Be the Controller.**

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Python](https://img.shields.io/badge/python-3.11%2B-blue)
![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Windows-lightgrey)

**CV_to_StreetFighter** is a Python-based fighting game engine that blends classic arcade mechanics with modern Computer Vision. Control your character using **real-time body movements** captured by your webcam, facing off against a keyboard-controlled opponent in a high-tech robotic arena.

---

## 🚀 Features

### 🤖 Robotics Theme Overhaul
*   **New Arena**: Battle in the **Blue Robotic Arena**, a futuristic grid combat zone.
*   **Characters**: Play as **Cyber Ryu** and **Mecha Ken**.
*   **UI**: Enhanced Sci-Fi HUD with Cyan Health bars and Neon Purple Super bars.

### 🎮 Hybrid Control System
The game is configured for a unique **Asymmetric Multiplayer** experience:

#### **Player 1: Cyber Ryu (Human Controlled)**
*Controlled via Webcam & Computer Vision* 📸

*   **Movement (Virtual Joystick)**:
    *   **Step LEFT** in camera frame → Walk Left ⬅️
    *   **Step RIGHT** in camera frame → Walk Right ➡️
    *   **Stand CENTER** → Stop/Idle ⏹️
*   **Combat Gestures**:
    *   **Punch**: Raise wrist to shoulder height (or extend arm) 👊
    *   **Kick**: Lift one leg significantly off the ground 🦶
*   **Tech Stack**: Powered by a **Hybrid System** (LSTM AI Model + Geometric Heuristics) for maximum responsiveness.

#### **Player 2: Mecha Ken (Keyboard Controlled)**
*Controlled via Standard Keyboard* ⌨️

*   **Move**: Arrow Keys ⬆️⬇️⬅️➡️
*   **Attack**: Keys `A`, `S`, `D` (Punchess) / `Z`, `X`, `C` (Kicks)

---

## 🛠️ Installation

### 1. Clone the Repository
```bash
git clone https://github.com/Coder-NehaSharma/CV_to_StreetFighter.git
cd CV_to_StreetFighter
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```
*   **Required**: `pygame`, `PyOpenGL`, `opencv-python`, `mediapipe`, `numpy`, `torch`

---

## 🕹️ How to Play

### Run the Game
```bash
python main.py
```

### The Setup
1.  **Camera**: Ensure your webcam is connected.
2.  **Position**: Stand back so your full body (or at least upper body + legs) is visible.
3.  **Launch**: The game will launch into the "Versus" screen immediately.

### Fighting Tips
*   Use your **body** to dodge and weave.
*   Step in to attack, step back to retreat.
*   Unleash punches and kicks physically!

---

## 🔧 Technical Details

*   **Language**: Python 3.11+
*   **Rendering**: Pygame + PyOpenGL (Hardware Accelerated)
*   **Vision Pipeline**:
    *   **MediaPipe**: High-speed skeletal tracking.
    *   **LSTM**: Temporal gesture recognition.
    *   **Heuristics**: Real-time geometric analysis for latency-free twitch reactions.
*   **Asset Pipeline**: JSON-based frame data engine supporting complex state machines (Hitstun, Blockstun, Parries).

---

<p align="center">
  Created by <a href="https://github.com/Coder-NehaSharma">Coder-NehaSharma</a>
</p>
