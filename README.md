# Parking Spot Detector and Classifier

## Overview

A classical image processing system that automatically detects and classifies parking spots as occupied or empty. The system uses edge detection, morphological operations, and grid line analysis to identify parking spaces, then applies intensity and texture-based features to determine occupancy status.

## Steps to Run

1. Install required dependencies:
```bash
python3 -m venv venv
source /venv/bin/activate
pip install -r requirements.txt
```

2. Organize your parking lot images in the following structure:
```
sets/
├── easy/
├── medium/
└── hard/
```

3. Run the notebook using Jupyter/VS Code

## Pipeline
![pipeline](pipeline.png)
1. **Preprocessing**: 
   - Converts input images to grayscale
   - Applies Gaussian blur (5×5 kernel) for noise reduction
   - Enhances contrast using CLAHE with 8×8 tile grid

2. **Edge Detection**: 
   - Computes Sobel gradients in X and Y directions
   - Calculates gradient magnitude for edge strength
   - Applies Canny edge detector (thresholds: 30-100)

3. **Grid Formation**: 
   - Extracts horizontal lines using morphological opening (40×1 kernel)
   - Extracts vertical lines using morphological opening (1×40 kernel)
   - Applies probabilistic Hough transform to detect line segments
   - Uses Gaussian smoothing and peak detection to locate row/column markers

4. **Slot Detection**: 
   - Merges row and column markers into a grid structure
   - Filters grid cells based on size constraints
   - Generates bounding boxes for individual parking spaces

5. **Classification**: 
   - Extracts multiple features per slot:
     - Mean intensity and standard deviation
     - Edge density from Canny detection
     - Dark/bright pixel ratios
     - Local texture variance
   - Computes occupancy score based on weighted features
   - Classifies as occupied if score ≥ 2

6. **Visualization**: 
   - Draws yellow boxes around all detected parking spots
   - Adds red inner boxes for occupied spaces
   - Marks corner points with red circles

## Output

### Easy Difficulty
![Easy 20](output/1_20.png)
![Easy 29](output/1_29.png)
![Easy](output/1_easy.jpg)
![Not That Easy](output/1_not_that_easy.jpg)

![Easy 29 - Second ROI](output/2_29.png)
![Easy - Second ROI](output/2_easy.jpg)

### Medium Difficulty
![Medium 12](output/1_12.png)
![Medium 31](output/1_31.png)
![Medium 30](output/1_30.png)

![Medium 12 - Second ROI](output/2_12.png)
![Medium 31 - Second ROI](output/2_31.png)

### Hard Difficulty
![Hard 21](output/1_21.png)
![Hard Frame 1](output/1_frame1.jpg)
![Hard Frame 600](output/1_frame600.jpg)

![Hard Frame 1 - ROI 2](output/2_frame1.jpg)
![Hard Frame 600 - ROI 2](output/2_frame600.jpg)

![Hard Frame 1 - ROI 3](output/3_frame1.jpg)
![Hard Frame 600 - ROI 3](output/3_frame600.jpg)

![Hard Frame 1 - ROI 4](output/4_frame1.jpg)

![Hard Frame 1 - ROI 5](output/5_frame1.jpg)

![Hard Frame 1 - ROI 6](output/6_frame1.jpg)

---

**Author**: Tanush Rajkumar  
