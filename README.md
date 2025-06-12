# 🎾 Tennis Player Tracking with Court Verification

This project tracks two tennis players in a match video using YOLOv8 and Deep SORT, calculates their total movement in meters, and intelligently avoids tracking during non-game camera angles (e.g., replays, close-ups).

## 📌 Project Objectives

- Detect and track both tennis players throughout a match.
- Accurately compute how much each player moves (in meters).
- Ignore frames where the court is not fully visible (camera cuts, zoom-ins).
- Output an annotated video with bounding boxes, trails, and distance data.

## 🧠 Approach & Logic

1. **Detection**: YOLOv8 detects people in every frame.
2. **Tracking**: Deep SORT assigns consistent IDs across frames.
3. **Filtering**: Tracks must persist long enough to be considered players.
4. **Court Check**: Edge + Hough Line detection ensures only valid full-court views are analyzed.
5. **Distance Calculation**: Movement in pixels converted to meters.
6. **Annotation**: Results overlaid on video and saved.

## 🚀 How to Run

1. Clone the repository or unzip this folder.
2. Install dependencies:
```bash
pip install -r requirements.txt
```
3. Place your input video as `tennis_video_assignment.mp4` in the same directory.
4. Run:
```bash
python tennis_tracking_with_court_verification.py
```

## 📦 Dependencies

- ultralytics
- opencv-python
- deep_sort_realtime
- scikit-image
- numpy

## ⚠️ Key Assumptions

- First frame shows a full-court angle.
- Players appear longer than any non-player.
- Known pixel-to-meter calibration is used.
- Input is a clean tennis match video.

## 🚧 Challenges

- Handling non-game camera views
- Avoiding false positives in replays
- SSIM false negatives resolved by using court geometry detection

---
