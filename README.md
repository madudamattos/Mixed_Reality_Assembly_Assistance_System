# Augmented Tangram: MR-Assisted Assembly System

This repository contains the source code and assets for the **Augmented Tangram**, a Mixed Reality (MR) application designed to simulate and assist manual assembly tasks. The system utilizes the **Meta Quest 3** headset to track physical Tangram pieces in real-time. It provides procedural assistance, instantaneous validation, and audio-visual feedback to reduce the user's mental workload and enhance engagement during assembly.

---

## 🛠️ Technical Architecture

### System Stack

| Component | Details |
|---|---|
| **Engine** | Unity 6000.38f |
| **Hardware** | Meta Quest 3 |
| **Interaction Library** | Meta SDK v77.0.0 |
| **Tracking Library** | OpenCV for Unity v2.6.0 |
| **Detection Method** | ArUco Markers — 4X4_50 DICT, 0.022m marker size |

### How It Works

The ArUco tracking system in this repository is an extension of the work by [Takashi Yoshinaga](https://github.com/TakashiYoshinaga/QuestArUcoMarkerTracking), distributed under the MIT License.

Building on his ArUco detection pipeline, this project adds **multi-marker detection**, improved tracking quality, a full **Tangram validation logic**, and **Meta Quest 3 passthrough integration**.

The core of the application relies on a continuous comparison between the user's physical manipulation and a predefined digital **Goal State** (`vTemplate`):

1. **Image Acquisition** — The system accesses the Meta Quest 3's native passthrough 2D image stream via the Meta SDK.
2. **Marker Detection** — The OpenCV for Unity plugin processes the feed to detect ArUco markers attached to each physical piece.
3. **Spatial Mapping** — The system computes transformation matrices to determine the 3D pose (position and rotation) of each piece in physical space, creating a **digital twin** of each piece.
4. **Real-time Validation** — The system continuously compares the current pose of each virtual piece against its target slot in the virtual template.

---

## 🎮 Features & Interaction

### 1. Intelligent Feedback

To accommodate tracking noise and physical inaccuracies, the system applies a tolerance threshold for validation:

- **Radial deviation:** < 0.5 cm
- **Rotational deviation:** < 10°

Once a piece enters this threshold, it triggers audio-visual reinforcement — illuminating the slot and locking the piece's color.

### 2. Situated Guidance (Hint System)

Users can access a **"Hint" (DICA) button** via natural hand gestures. Interaction is managed through the Quest 3's native hand-tracking, detecting collisions between the virtual hand model and UI components.

> **How to use:** Hold the desired piece, then press the button. The system will reveal the correct final orientation for the last selected piece.

### 3. User Experience

- **Controller-free** experience designed for direct object manipulation — users handle physical pieces naturally.
- **Gamification** elements include celebratory visual effects triggered upon task completion, intended to boost positive affect and flow.

---

## 🚀 Getting Started

### Installation

1. Clone the repository.
2. Open the project in **Unity**.
3. Build and run on **Meta Quest 3**.

### Calibration

**Step 1 — Environment Setup (Recommended)**

Map the environment using the Quest 3's native spatial mapping system. Make sure there is exactly **one object with the "table" anchor** in the scene. This step is optional but highly recommended.

**Step 2 — In-App Calibration**

Launch the application. It will start in the internal calibration stage. Use the following controls to position the setup correctly on the table:

| Control | Action |
|---|---|
| **Button A** (right controller) | Close the debug screen if it opens on startup |
| **Button B** (right controller) | Toggle the ArUco camera debug view — shows detected marker outlines and IDs to verify detection |
| **Right thumbstick** | Move the virtual template across the table surface |
| **Left thumbstick** | Rotate the virtual template around the vertical (UP) axis |
| **Button X** | Move the template up |
| **Button Y** | Move the template down |

**Step 3 — Finish Calibration**

Set the controllers down on a surface and press the black **"CALIBRATION"** button with one of your hands to complete the calibration process.

### You're ready to play! 🎉

---


## 🔗 Reference Repositories

This implementation is based on the following sample repositories:

- [QuestArUcoMarkerTracking](https://github.com/TakashiYoshinaga/QuestArUcoMarkerTracking) — by Takashi Yoshinaga
- [Unity-PassthroughCameraApiSamples](https://github.com/oculus-samples/Unity-PassthroughCameraApiSamples)
