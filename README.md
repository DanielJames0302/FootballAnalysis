# Football Analysis System

A comprehensive computer vision-based football video analysis system that tracks players, referees, and the ball, estimates speeds and distances, assigns teams, and analyzes camera movements in football matches.

## 🚀 Features

### Core Functionality
- **Multi-Object Tracking**: Tracks players, referees, and the ball using YOLOv8 and ByteTrack
- **Team Assignment**: Automatically assigns players to teams using color-based clustering
- **Ball Possession**: Determines which player has possession of the ball
- **Speed & Distance Estimation**: Calculates player speeds and total distance covered
- **Camera Movement Analysis**: Estimates and compensates for camera movements
- **View Transformation**: Transforms camera view to top-down perspective for accurate measurements
- **Video Output**: Generates annotated videos with all analysis overlays

### Technical Capabilities
- Real-time object detection and tracking
- Position interpolation for smooth ball tracking
- Perspective transformation for accurate distance measurements
- Camera movement compensation
- Team color-based player classification
- Speed and distance calculations in real-world units

## 📁 Project Structure

```
FootballAnalysis/
├── main.py                          # Main execution script
├── yolo_inference.py               # YOLO model inference script
├── models/                         # Trained YOLO models
│   ├── best.pt
│   └── last.pt
├── trackers/                       # Object tracking module
│   ├── __init__.py
│   └── tracker.py
├── team_assigner/                  # Team assignment module
│   ├── __init__.py
│   └── team_assigner.py
├── player_ball_assigner/           # Ball possession assignment
│   ├── __init__.py
│   └── player_ball_assigner.py
├── camera_movement_estimator/      # Camera movement analysis
│   ├── __init__.py
│   └── camera_movement_estimator.py
├── view_transformer/               # Perspective transformation
│   ├── __init__.py
│   └── view_transformer.py
├── speed_and_distance_estimator/   # Speed and distance calculations
│   ├── __init__.py
│   └── speed_and_distance_estimator.py
├── utils/                          # Utility functions
│   ├── __init__.py
│   ├── bbox_utils.py
│   └── video_utils.py
├── stubs/                          # Cached analysis data
│   ├── camera_movement_stub.pkl
│   └── track_stubs.pkl
├── output_videos/                  # Generated output videos
│   └── output_video.avi
└── development_and_analysis/       # Development notebooks
    └── color_assignment.ipynb
```

## 🛠️ Installation

### Prerequisites
- Python 3.8+
- CUDA-compatible GPU (recommended for faster processing)

### Dependencies
```bash
pip install ultralytics
pip install supervision
pip install opencv-python
pip install numpy
pip install pandas
pip install scikit-learn
```

### Model Setup
1. Download the YOLOv8 model file (`yolov8m.pt`) or use your custom trained model
2. Place the model file in the `models/` directory
3. Update the model path in `main.py` if using a different model

## 🎯 Usage

### Basic Usage
```bash
python main.py
```

### Input Requirements
- Place your football video file in the `input_videos/` directory
- Update the video path in `main.py` (currently set to `'input_videos/08fd33_4.mp4'`)

### Output
The system generates an annotated video in `output_videos/output_video.avi` containing:
- Player tracking with team assignments
- Ball tracking and possession indicators
- Speed and distance overlays
- Camera movement information
- Team ball control visualization

## 🔧 Configuration

### Model Configuration
- **Model Path**: Update `model_path` in `main.py` to use your preferred YOLO model
- **Confidence Threshold**: Adjust detection confidence in `tracker.py`

### Analysis Parameters
- **Frame Window**: Speed calculation window (default: 5 frames)
- **Frame Rate**: Video frame rate for speed calculations (default: 24 fps)
- **Max Ball Distance**: Maximum distance for ball-player assignment (default: 70 pixels)
- **Camera Movement Threshold**: Minimum distance for camera movement detection

### View Transformation
The system uses a perspective transformation to convert camera view to top-down view:
- **Court Dimensions**: 68m width × 23.32m length
- **Pixel Vertices**: Calibrated for specific camera setup
- **Target Vertices**: Real-world court coordinates

## 📊 Analysis Components

### 1. Object Detection & Tracking
- Uses YOLOv8 for object detection
- ByteTrack algorithm for multi-object tracking
- Tracks players, referees, and ball separately
- Handles object occlusion and re-identification

### 2. Team Assignment
- Color-based clustering using K-means
- Analyzes player jersey colors in top half of bounding boxes
- Assigns players to two teams based on dominant colors
- Maintains team consistency across frames

### 3. Ball Possession
- Calculates distance between ball and each player
- Assigns ball to closest player within threshold distance
- Tracks team ball control throughout the match

### 4. Speed & Distance Estimation
- Calculates player speeds using position changes over time
- Converts pixel distances to real-world measurements
- Displays speed in km/h and total distance in meters
- Updates measurements every 5 frames

### 5. Camera Movement Analysis
- Uses optical flow to detect camera movements
- Compensates for camera motion in position calculations
- Improves accuracy of speed and distance measurements
- Caches movement data for faster processing

### 6. View Transformation
- Transforms camera perspective to top-down view
- Enables accurate real-world distance measurements
- Uses homography transformation matrix
- Filters points outside the court boundaries

## 🎥 Output Features

The generated video includes:
- **Player Tracking**: Bounding boxes with team colors
- **Ball Tracking**: Ball position and trajectory
- **Speed Display**: Real-time speed for each player
- **Distance Display**: Total distance covered by each player
- **Team Control**: Visual indicator of which team has ball possession
- **Camera Movement**: Overlay showing camera movement information

## 🔄 Processing Pipeline

1. **Video Input**: Load and process video frames
2. **Object Detection**: Detect players, referees, and ball using YOLO
3. **Tracking**: Track objects across frames using ByteTrack
4. **Camera Movement**: Estimate and compensate for camera motion
5. **View Transformation**: Transform to top-down perspective
6. **Team Assignment**: Assign players to teams based on colors
7. **Ball Possession**: Determine which player has the ball
8. **Speed Calculation**: Calculate speeds and distances
9. **Visualization**: Draw annotations and overlays
10. **Output**: Save annotated video

## 🚀 Performance Optimization

- **Batch Processing**: Processes frames in batches for efficient GPU usage
- **Caching**: Saves tracking and camera movement data to avoid recomputation
- **Interpolation**: Smooths ball tracking with position interpolation
- **Selective Processing**: Skips unnecessary calculations for referees and ball

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- **YOLOv8**: For object detection capabilities
- **ByteTrack**: For multi-object tracking
- **OpenCV**: For computer vision operations
- **Supervision**: For detection and tracking utilities

## 📞 Support

For questions, issues, or contributions, please open an issue on the GitHub repository.

---

**Note**: This system is designed for football match analysis and may require calibration for different camera setups and field configurations. 