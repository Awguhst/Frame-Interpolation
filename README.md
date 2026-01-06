# Video Frame Interpolation with Lightweight U-Net

## What is Video Frame Interpolation?

Video frame interpolation is a technique that generates new **intermediate frames** between two existing consecutive frames in a video. This creates the illusion of smoother motion and effectively increases the frame rate (e.g., from 30 FPS to 60 FPS) without changing the playback speed.

Why is it useful?
- Turns choppy low-FPS videos into buttery-smooth high-FPS ones
- Enables convincing slow-motion from normal-speed footage
- Improves visual quality for old videos, games, or compressed content

Traditional methods (like simple blending) often produce ghosting or blurry artifacts. Modern deep learning approaches, like this U-Net model, learn complex motion patterns to synthesize realistic in-between frames with sharp details and accurate object movement.

## Project Overview
A simple yet effective U-Net model trained on the Vimeo-90K dataset. It takes two consecutive frames as input and predicts a high-quality middle frame, enabling smooth video frame rate upsampling while preserving motion continuity and minimizing visual artifacts.

## Live Demo
Try the CPU-only Gradio app deployed on Hugging Face Spaces:  
[https://huggingface.co/spaces/your-username/video-frame-interpolation-demo](https://huggingface.co/spaces/your-username/video-frame-interpolation-demo)  
*(Replace with your actual Space link)*

Upload any video, interpolate frames, and download the smoother version with original audio preserved.

## Demo Comparison

### Original (30 FPS) vs Interpolated (60 FPS)

| Original Video | Interpolated Video (2× smoother) |
|---------------|--------------------------------|
| <video src="original_video.mp4" controls muted width="400"></video> | <video src="interpolated_video_with_audio.mp4" controls width="400"></video> |

*(Embed your actual video files or use side-by-side GIFs/embedded videos here)*

## Model Architecture
- Lightweight U-Net with double convolutions (GELU activation)
- Input: Concatenated frame1 + frame2 (6 channels)
- Output: Predicted middle frame (3 channels)
- Skip connections and transpose convolutions for precise alignment

## Training Details
- Dataset: Vimeo-90K triplet (subsets used for faster iteration)
- Optimizer: Adam (lr=1e-4)
- Scheduler: ReduceLROnPlateau
- Early stopping + best model checkpointing

## Inference Usage
The provided script includes:
- Loading a video
- Interpolating frames pairwise
- Doubling FPS while keeping original speed
- Re-adding original audio via ffmpeg

Perfect for creating buttery-smooth slow-motion or frame-rate upsampling effects.

Enjoy smoother videos! 🚀
