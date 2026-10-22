# Namma Space - 3D Web Walkthrough from Phone Video

An end-to-end spatial engine pipeline that converts standard smartphone video captures of indoor environments into photorealistic, interactive 3D digital twins, viewable directly in a web browser with zero installation.

## 🌐 Live Demo
Experience the 3D web viewer here: 
**[Click to View the Live Room](https://mshreyas3213-design.github.io/namma-space/viewer/index.html?splat=./room1_small.splat)**

## 🏗️ System Architecture
Our pipeline consists of 5 main stages:
1. **Data Capture:** Smartphone video following our custom SOP (locked exposure, 3-ring trajectory).
2. **Frame Extraction:** FFmpeg extracts frames at 2 FPS.
3. **Pose Estimation:** COLMAP (Structure-from-Motion) recovers camera poses.
4. **3D Reconstruction:** 3D Gaussian Splatting (3DGS) generates the photorealistic `.ply` model.
5. **Optimization & Deployment:** The model is decimated and compressed to a `.splat` format (< 10MB) and rendered using Three.js and the Spark Renderer.

## 📋 Prerequisites
To run this pipeline locally, you will need:
*   **COLMAP** (for Structure-from-Motion)
*   **FFmpeg** (for video frame extraction)
*   **Python 3.8+** 
*   **Node.js & npm** (for the `splat-transform` tool)
*   **3DGS Repository** (e.g., Inria 3DGS or gsplat) for training the model.

## 🚀 How to Reconstruct and View

### 1. Extract Frames
Extract frames from your video at 2 frames per second:
```bash
ffmpeg -i video.mp4 -vf "fps=2" -q:v 2 frames/frame_%04d.jpg
