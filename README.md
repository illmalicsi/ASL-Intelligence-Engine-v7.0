# ASL Intelligence Engine v7.0

This is a high-performance, browser-based **American Sign Language (ASL)** recognition system. It leverages **MediaPipe** for high-fidelity hand tracking, **Three.js** for real-time 3D skeletal visualization, and a custom **k-Nearest Neighbors (k-NN)** algorithm for gesture classification.

The engine features a dual-mode interface allowing users to either recognize pre-trained signs or build their own gesture dataset through an integrated training suite.

---

## 🚀 Key Features

* **Real-time Recognition**: Classifies ASL alphabet signs with low latency using a k-NN classification algorithm ().
* **3D Neural HUD**: A Picture-in-Picture (PiP) window rendered with Three.js that displays a smoothed 3D representation of the hand's skeletal structure.
* **Custom Training Suite**: Capture your own samples to train the engine for specific hand shapes or environments.
* **Model Persistence**: Export your trained dataset as a `.json` file and import it later or share it with others.
* **Cyberpunk Aesthetic**: A high-contrast, neon-themed UI designed for clarity and visual impact.

---

## 🛠 Tech Stack

* **Core**: HTML5, CSS3 (Custom Variables/Grid), Vanilla JavaScript (ES6+).
* **AI/ML**: [MediaPipe Hands](https://www.google.com/search?q=https://google.github.io/mediapipe/solutions/hands.html) for landmark detection.
* **Graphics**: [Three.js](https://threejs.org/) (WebGL) for 3D skeleton rendering.
* **Logic**: Custom k-NN implementation using Euclidean distance normalization.

---

## 🕹 How to Use

### 1. Recognition Mode (Default)

Position your hand in front of the webcam. The engine will compare your hand's landmarks against the current dataset.

* **Match Quality**: Displayed in the central HUD.
* **Confidence Bar**: Visualizes how closely your pose matches the closest known sample.

### 2. Training Mode

Switch to Training mode via the top toggle or by pressing `TAB`.

1. **Enter Letter**: Type the character (A-Z) you wish to train.
2. **Select Sample Mode**: Choose how many snapshots to take (e.g., "5 Samples" for better accuracy).
3. **Capture**: Press `SPACE` to snap a pose. The engine normalizes coordinates relative to the wrist to ensure distance/scaling doesn't break the model.

### ⌨️ Keyboard Shortcuts

| Key | Action |
| --- | --- |
| `TAB` | Toggle between **Recognition** and **Training** modes |
| `SPACE` | Capture a training sample (Training mode only) |
| `ESC` | Reset the current detection display |

---

## 📐 The Classification Logic

The engine uses a distance-based classification approach:

1. **Normalization**: Landmark coordinates are translated so the wrist (Landmark 0) sits at .
2. **Euclidean Distance**: The system calculates the sum of distances between the 21 live landmarks and the stored samples.


3. **k-NN Voting**: The 3 closest samples "vote" on the identity of the current pose.
4. **Thresholding**: If the distance exceeds **1.5**, the engine rejects the match as "Unknown" to prevent false positives.

---

## 💾 Data Management

* **LocalStorage**: Your training data is automatically saved to the browser's local storage.
* **Export**: Click **Export Model** to download a `.json` file containing your entire gesture dataset.
* **Import**: Use **Import Model** to load a previously saved dataset or merge new data into your current session.
