# Tennis Player Tracker 🎾

This project tracks tennis players in a match using a custom-trained YOLO model (to detect players with rackets), Deep SORT for tracking them over time, and some basic geometry to make sure we only track when the camera is showing the full court.

---

## What it does

- Detects players holding rackets using a custom YOLOv8 model
- Tracks their positions consistently using Deep SORT
- Measures how far each player moves (in meters)
- Skips tracking during replays, close-ups, or zoomed-in scenes
- Outputs a video with bounding boxes, player labels, and distance traveled

---

## Why a custom model?

Most pretrained YOLO models detect "person", which includes ball kids, umpires, etc.  
With a custom model trained specifically to detect **players with rackets**, we get much cleaner and more relevant results.

---

## How it works

1. YOLO detects players in each frame
2. Deep SORT tracks them across frames and assigns unique IDs
3. We calculate how far each tracked player moves
4. Canny + Hough line detection checks if the camera angle is valid (i.e., shows the court)
5. If the scene is valid, we annotate and track. If not, we pause tracking.

---

## To run

1. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

2. Add your input video and name it:

   ```
   tennis_video_assignment.mp4
   ```

3. Replace the YOLO model path:

   ```python
   YOLO_MODEL = 'your_custom_model.pt'
   ```

4. Run the script:

   ```bash
   python tennis_tracking_with_court_verification.py
   ```

You’ll get an output video named `output_annotated.mp4` with everything drawn on it.

---

## Dependencies

- ultralytics
- opencv-python
- deep_sort_realtime
- scikit-image
- numpy

---

## Notes

- The script assumes the first frame shows the full court.
- Distance is calculated using the width of a standard singles court (8.23 meters).
- You can fine-tune the line detection parameters if it misses valid scenes.

---

## Difficulty Faced

- The model needed a big training set which could be obtained by manually saving frames and marking player with racket.
- The player closer to camera is nicely visible hence could be identified easily but doesn't goes the same for away player due to input video quality.

