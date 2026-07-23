# Eye Controlled Virtual Mouse

Control your mouse cursor and perform clicks using just your eyes and a webcam! This project uses real-time facial landmark detection to track your iris position and eye blinks, translating them into mouse movement and click actions.

## Summary

A computer vision–based virtual mouse that enables hands-free cursor control and mouse clicks using real-time eye tracking with OpenCV, MediaPipe, and PyAutoGUI.

## How It Works

1. **Webcam Capture** — Continuously captures video frames from your default camera.
2. **Face Mesh Detection** — Uses MediaPipe's Face Mesh (with iris refinement enabled) to detect 478 facial landmarks per frame, including detailed iris landmarks.
3. **Cursor Movement** — Tracks the right iris landmarks (indices 474–477) and maps their position on the video frame to a corresponding position on your screen using `pyautogui`.
4. **Blink Detection (Click)** — Monitors the vertical distance between the upper and lower eyelid landmarks (indices 159 and 145). When the eyelids get close enough together (indicating a blink), it triggers a mouse click.
5. **Visual Feedback** — Draws green circles on the iris landmarks and yellow circles on the eyelid landmarks over the live video feed so you can see what's being tracked.

## Requirements

- Python 3.7+
- A working webcam
- The following Python packages:
  - `opencv-python`
  - `mediapipe`
  - `pyautogui`

## Installation

Clone the repo and install dependencies from `requirements.txt`:

```bash
git clone https://github.com/pragna1509/virtual-mouse-using-eye-tracking.git
cd virtual-mouse-using-eye-tracking
pip install -r requirements.txt
```

## Usage

1. Make sure your webcam is connected and accessible.
2. Run the script:
   ```bash
   python eye_controlled_mouse.py
   ```
3. A window titled **"Eye Controlled Mouse1"** will open, showing your webcam feed with tracking points overlaid.
4. Move your eyes to move the cursor around the screen.
5. Blink (close your eyes briefly) to perform a mouse click.
6. Press **`q`** while the video window is focused to quit the program cleanly.

## Known Issues & Suggested Improvements

- **Sensitive blink threshold** — The blink detection threshold (`0.004`) is very tight and may need tuning based on your camera resolution, distance from the screen, and lighting conditions.
- **No error handling for missing camera frames** — `cam.read()` can occasionally return `False`; consider checking the returned boolean before processing.
- **Click cooldown** — `pyautogui.sleep(1)` pauses click detection for 1 second after a click to help prevent accidental double-clicks, but this also briefly freezes cursor movement. You can decouple this if needed.
- **Jittery cursor** — Since single-frame iris positions can be noisy, consider smoothing cursor movement (e.g., a moving average or exponential smoothing) for a steadier experience.

## Project Structure

```
.
├── eye_controlled_mouse.py   # Main script
├── requirements.txt          # Python dependencies
├── .gitignore                # Files/folders excluded from git
└── README.md                 # This file
```
## Technologies Used

- Python
- OpenCV
- MediaPipe
- PyAutoGUI
- Computer Vision


## Features

- Real-time eye tracking 
- Hands-free cursor control
- Blink detection for mouse clicks
- Webcam-based interaction
- Lightweight Python implementation


## Disclaimer

This is a basic prototype intended for learning and experimentation with computer vision and accessibility tech. It is not intended for production or medical/assistive use without further testing, calibration, and safety safeguards (e.g., a manual override or pause key).
