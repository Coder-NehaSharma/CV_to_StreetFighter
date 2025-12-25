# CV_to_StreetFighter: Comprehensive Project Guide

**Version:** 2.0 (Robotics & Stability Update)
**Date:** December 2025
**Author:** Coder-NehaSharma

---

## 1. Project Vision & Overview
**"Fight the Future. Be the Controller."**

This project bridges the gap between physical movement and digital combat. Unlike traditional motion games that rely on handheld controllers (Wii, VR wands), **CV_to_StreetFighter** uses advanced Computer Vision (CV) to map your full body directly into the game.

The goal is to create a Controller-Free Fighting Game Engine that is responsive, intuitive, and accessible. The current iteration features a "Robotics Theme" where players control a Cybernetic warrior using their own body.

---

## 2. User Manual (How to Play)

### 2.1 Setup & Calibration
*   **Environment:** Ensure you have a clear space (approx. 6x6 feet) and decent lighting.
*   **Camera:** Place your webcam at chest height. Step back until your upper body and knees/ankles are visible.
*   **Launch:** Run `python main.py`.

### 2.2 Controls (Player 1 - Human)
You control **Cyber Ryu** on the left side of the screen.

| Action | Physical Movement |
| :--- | :--- |
| **Walk Left** | Step to the **LEFT** side of your camera frame (Zone < 35%). |
| **Walk Right** | Step to the **RIGHT** side of your camera frame (Zone > 65%). |
| **Stop** | Return to the **CENTER** of the frame. |
| **Punch** | Raise your fist to shoulder height or extend your arm forward. |
| **Kick** | Lift one leg significantly (knee up or side kick). |

> **Pro Tip:** The system uses a "Virtual Joystick". Think of your room as the d-pad. Step left to go left, center to stop.

### 2.3 Controls (Player 2 - Opponent)
Use the **Keyboard** to control **Mecha Ken**.

*   **Move:** Arrow Keys `⬆️` `⬇️` `⬅️` `➡️`
*   **Attack:** `A`, `S`, `D` (Punch) / `Z`, `X`, `C` (Kick)

---

## 3. Technical Deep Dive (How It Works)

### 3.1 The Vision Pipeline (`pose_worker.py`)
This is the brain of the operation. It runs on a separate thread to maintain high FPS.

1.  **Capture:** Reads raw frames from Webcam (OpenCV).
2.  **Inference:** Uses **MediaPipe Pose** to extract 33 skeletal landmarks (Shoulders, Elbows, Wrists, Hips, Knees, Ankles).
3.  **Optimization:** Filters down to 21 key points for speed.
4.  **Logic Layer:**
    *   **Virtual Joystick:** Calculates the `center_x` of the user. If `center_x < 0.35`, send "LEFT" command.
    *   **Heuristics:** Analyzes geometric relationships in real-time.
    *   **Punch Check:** `abs(Wrist_Y - Shoulder_Y) < Threshold`
    *   **Kick Check:** `abs(Left_Ankle_Y - Right_Ankle_Y) > Threshold`
5.  **Output:** Pushes specific game commands (Left, Right, Button 1, Button 4) to a thread-safe Queue.

### 3.2 The Game Engine (`main.py` & `Active_Objects.py`)
Built on Pygame (Input/Audio) and PyOpenGL (Rendering).

*   **State Machine:** Every character action (Stand, Walk, Punch) is a "State". The engine manages transitions (e.g., cannot Walk while Punching).
*   **Frame Data:** Animations are defined by "frames" in JSON files, specifying duration, hitbox size, and velocity. This allows for arcade-perfect timing (hitstun, blockstun).
*   **Collision:** Uses precise Box Collision (Hurtbox vs Hitbox). A punch only connects if the **Red Hitbox** overlaps the opponent's **Green Hurtbox**.

---

## 4. Real-World Applications
This technology extends far beyond a simple fighting game:

### 4.1 Fitness & Exergaming
*   **Cardio Combat:** Gamify martial arts training. Users burn calories by physically dodging and striking.
*   **Rehabilitation:** Adjust detection thresholds to encourage specific movements for physical therapy (e.g., "Raise arm to X height to score").

### 4.2 Immersive Arcades
*   **Touchless Interface:** ideal for public kiosks where hygiene is a concern.
*   **Low Cost:** Requires only a standard webcam, no expensive sensors or suits.

### 4.3 Accessibility
*   **Hands-Free Gaming:** Allows players with limited hand dexterity to play using gross motor movements of the head or torso.

---

## 5. Future Roadmap (Advanced Gaming)

### 5.1 Full 3D Integration
*   **Unity/Unreal Bridge:** Send the skeletal data via UDP/OSC to a Unity game engine. This would allow controlling a high-fidelity 3D avatar in a AAA environment.

### 5.2 Networked Multiplayer
*   **Remote Dojo:** Two players in different houses fighting each other.
*   **Challenge:** Synchronizing physics over the internet (Rollback Netcode) while handling CV latency.

### 5.3 Advanced AI Moves
*   **Gestures:** Detect complex motions like "Hadouken" (Cupping hands and pushing) using improved LSTM models.
*   **Defense:** Detect "Blocking" by crossing arms or covering face.

### 5.4 Smart Calibration
*   **Auto-Zone:** The game could automatically detect the player's room size and adjust the "Left/Right" zones dynamically.
