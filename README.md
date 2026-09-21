<div align="center">

# 🎮 AirBlocks — Hand-Gesture Block Puzzle

**Play a block puzzle with nothing but your webcam and your bare hands.**

AirBlocks turns your camera into a controller. Powered by real-time
[MediaPipe](https://developers.google.com/mediapipe) hand-tracking, it reads your
finger gestures — **pinch/close to grab** a block and **open your hand to drop it** —
so you can fill rows and columns, clear lines, and chase a high score without ever
touching your keyboard or mouse.

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-3.x-000000?logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![MediaPipe](https://img.shields.io/badge/MediaPipe-HandLandmarker-00A6A6)](https://developers.google.com/mediapipe)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.9-5C3EE8?logo=opencv&logoColor=white)](https://opencv.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

</div>

---

## 📖 Overview

**AirBlocks** is an interactive, web-based block puzzle game controlled entirely
by hand gestures captured through your webcam. Instead of a keyboard or mouse, the
game uses **MediaPipe's Hand Landmarker** to track 21 points on your hand in real
time and interpret them as game commands.

The gameplay is simple and addictive: three random block shapes appear in a tray,
you **grab** one with a pinch or closed fist, move your hand to aim, and **release**
to drop it onto a 10×10 grid. Complete a full row or column to clear it and score
points. The game runs until no remaining block can fit anywhere on the board.

Under the hood, a Python **Flask** server captures your camera feed with **OpenCV**,
runs gesture inference on a background thread, and streams both the live video and
the game state to your browser — where the board is drawn on an HTML5 `<canvas>`.

> ### 🌐 Live Demo & Walkthrough
> - **▶️ Try the game:** [huggingface.co/spaces/britod/airblocks-handgesture-games](https://huggingface.co/spaces/britod/airblocks-handgesture-games)
> - **🎥 Watch how it works:** [Demo video](https://drive.google.com/file/d/1rzPOcpkYdnbqFuqbE1CfXpa-nOd3SOLO/view)

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🖐️ **Hands-free webcam control** | Play using only your camera — no keyboard or mouse needed. |
| 🤖 **MediaPipe hand-tracking** | Real-time detection of 21 hand landmarks via the MediaPipe Hand Landmarker model. |
| 🤏 **Pinch & release gestures** | **Grab** a block with a pinch or closed fist, then **open your hand** to place it. Two selectable grab modes: *Closed Fist* or *Pinch*. |
| 🧱 **Block placement** | Drag-and-drop 13 different block shapes (I, O, T, L, J, S, Z, squares, and more) onto a 10×10 grid. |
| 🏆 **Scoring & line clears** | Fill a complete row or column to clear it and earn **100 points** per line. Keep going until no block fits — then it's game over. |
| 🎯 **Adjustable ROI** | An on-screen Region-of-Interest box lets you frame exactly where your hand moves. |
| 📷 **Camera selector** | Switch between multiple connected cameras on the fly. |
| 📊 **Built-in metrics** | Tracks average FPS plus grab/drop accuracy and exports results to CSV. |

---

## 🕹️ How to Play

| Gesture | Action |
|---------|--------|
| 👋 Move hand | Aim the cursor across the board |
| ✊ Closed fist *(fist mode)* | Grab a block (hover the cursor over it first) |
| 🤏 Pinch *(pinch mode)* | 2- or 3-finger pinch to grab a block |
| 🖐️ Open hand | Drop / place the held block onto the grid |

1. Three random blocks appear in the tray at the bottom of the board.
2. Move your hand to hover the cursor over a block, then **grab** it.
3. Move to the grid and **release** to drop it on a valid, empty spot.
4. Fill an entire **row or column** to clear it and score points.
5. When no remaining block fits anywhere, it's **game over** — grab the **Retry**
   button to start a fresh round.

> **💡 Tuning tips:** Use the on-screen **ROI** box to frame where your hand moves,
> and the **Grab Gesture** selector to switch between *fist* and *pinch* modes for
> whatever feels most reliable with your camera and lighting.

---

## 🧰 Tech Stack

| Category | Technologies |
|----------|--------------|
| **Language** | Python 3.10+ |
| **Web Framework / Server** | Flask (MJPEG video stream + Server-Sent Events for game state) |
| **Computer Vision** | MediaPipe (Tasks Vision — Hand Landmarker), OpenCV |
| **Numerical / Data** | NumPy, pandas |
| **Analysis & Visualization** | Jupyter Notebook, Matplotlib, Seaborn, scikit-learn |
| **Frontend** | HTML5 Canvas, JavaScript, Jinja2 templates |
| **Model Asset** | `hand_landmarker.task` (MediaPipe pre-trained hand-landmark model) |

---

## 🚀 Getting Started

### Prerequisites

- **Python 3.10+**
- A **webcam** connected to your machine
- `pip` for installing dependencies

### Installation & Running

```bash
# 1. Clone the repository
git clone https://github.com/Vinn673/AirBlocks---Computer-Vision.git
cd AirBlocks---Computer-Vision

# 2. Move into the app folder
cd airblocks

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the server
python app.py
```

Then open **[http://localhost:5000](http://localhost:5000)** in your browser and
allow camera access. Frame your hand inside the green ROI box and start playing!

> **Note:** The webcam is captured on the machine running the server (via OpenCV's
> `cv2.VideoCapture`), so run this locally on a computer that has a camera.

### Optional Configuration (Environment Variables)

You can customize the defaults before launching `app.py`:

| Variable | Default | Purpose |
|----------|---------|---------|
| `CAMERA_INDEX` | `1` | Which camera to open first |
| `MAX_CAMERA_INDEX` | `5` | Highest camera index shown in the selector |
| `GRAB_MODE` | `fist` | Default grab gesture: `fist` or `pinch` |
| `ROI_X` / `ROI_Y` / `ROI_W` / `ROI_H` | `80 / 40 / 480 / 360` | Region-of-interest box for hand tracking |

---

## 🗂️ Project Structure

```
AirBlocks---Computer-Vision/
├── airblocks/                    # Flask web application
│   ├── app.py                    # Flask server + game logic + MediaPipe/OpenCV loops
│   ├── requirements.txt          # Python dependencies
│   ├── experiment_results.csv    # Exported gameplay metrics (FPS, grab/drop accuracy)
│   ├── templates/
│   │   └── index.html            # Browser UI (webcam feed + game canvas + controls)
│   └── README.md                 # App-specific notes
├── hand_landmarker.task          # MediaPipe hand-landmark model (~7.8 MB)
├── main.ipynb                    # Notebook: metrics evaluation & visualization
├── LICENSE                       # MIT License
└── README.md                     # ← you are here
```

---

## 🛠️ How It Works

The Flask server runs **two background threads** alongside the web app:

| Component | Role |
|-----------|------|
| **Thread 1 — Camera loop** | Reads the webcam, mirrors the frame, draws hand landmarks + the ROI box, and encodes JPEG frames at ~30 fps. |
| **Thread 2 — AI loop** | Crops the ROI, runs MediaPipe hand inference, interprets gestures, smooths the cursor, and updates the shared game state. |
| **`/camera`** | MJPEG stream — the browser `<img>` points here for the live video. |
| **`/state`** | Server-Sent Events — pushes JSON game state ~30×/s. |
| **`<canvas>`** | The browser redraws the board on every SSE update. |

Gesture detection is **geometry-based** on the 21 hand landmarks — counting open
fingers, measuring thumb/index (and thumb/middle) pinch distances, and detecting
open-hand releases. The cursor position is **exponentially smoothed** for stability.

---

## 📊 Metrics & Evaluation

During play, AirBlocks records experiment metrics and writes them to
`airblocks/experiment_results.csv` on exit (or on demand via the `/save_results`
endpoint):

- **Average FPS**
- **Grab** attempts, successes, and accuracy
- **Drop** attempts, successes, and accuracy
- **Overall success rate**

The `main.ipynb` notebook contains the evaluation and visualization workflow for
analyzing these results.

---

## 👥 Anggota Kelompok (Group Members)

> **Group 8 — LA01 · COMP7116001 — Computer Vision**

| # | Name | NIM | GitHub |
|:-:|------|-----|--------|
| 1 | **Brian Nicholas Tedjo** | 2802403183 | [@britoddd](https://github.com/britoddd) |
| 2 | **Jason Budiharjo** | 2802419446 | [@jason-b123](https://github.com/jason-b123) |
| 3 | **Justin Christian Kenan** | 2802399463 | [@jstn77](https://github.com/jstn77) |
| 4 | **Justin Christroper** | 2802420100 | — |
| 5 | **Kian Aurelio Wibowo** | 2802464582 | [@Kian76-IT](https://github.com/Kian76-IT) |
| 6 | **Marvin Adriano Rusdianto** | 2802402275 | [@Vinn673](https://github.com/Vinn673) |

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](./LICENSE)
file for details.

<div align="center">

*Made with 🖐️ and computer vision.*

</div>
