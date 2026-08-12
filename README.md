# MRI Audio-Video Sync Analysis

Automated detection of audio-video synchronization issues in 2,371 MRI videos.

# Overview
Analyzes large MRI video datasets to identify:

Audio-video sync delays (milliseconds to seconds)
Missing or silent audio tracks
Duration mismatches between video and audio
Results
Issue	Count	%
GOOD_SYNC (<200ms)	2,179	91.9%
MISSING_AUDIO	58	2.4%
DURATION_MISMATCH	1,524	64.3%
MINOR_DELAY	1	0.04%

<img width="2385" height="1771" alt="MRI Graphs" src="https://github.com/user-attachments/assets/b4e6aefc-0fe0-4be5-8247-bbd1aabd6b74" />

# Data Set

Source: Figshare - 2D Real-time MRI Videos (Multispeaker Speech Production Study)

The dataset contains 2,371 real-time MRI videos from a speech production study with multiple speakers. These videos are used to analyze audio-video synchronization issues.

# How It Works
Extract video metadata (FPS, duration) using OpenCV
Extract audio from videos using ffmpeg + librosa
Compute audio energy envelope (Mel-spectrogram)
Detect video motion (frame-to-frame differences)
Calculate sync offset using cross-correlation (scipy.signal)
Categorize issues by type and severity
Generate Excel report with results
Create visualization dashboard


Installation
bash
# Install dependencies
pip install -r requirements.txt

# Update dataset path in mri_sync_analyzer.py
DATASET_PATH = "/path/to/your/mri/videos"

# Run analysis
python Scripts/mri_sync_analyzer.py
Requirements
Python 3.8+
ffmpeg (for audio extraction)
opencv-python, librosa, scipy, pandas, openpyxl, matplotlib, seaborn
Output
Reports/MRI_Issues_Organized.xlsx - Detailed Excel report
Reports/MRI_Analysis_Charts.png - Visualization dashboard
Tech Stack

OpenCV | librosa | scipy.signal | pandas | openpyxl | matplotlib

Important Notes
Results are estimates based on cross-correlation, not ground truth
Manual verification recommended before production use
Works best for videos with clear motion and audio variation
May struggle with silent scenes or low quality audio

Author
Harsh Kumar
