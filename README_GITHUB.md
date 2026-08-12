# MRI Audio-Video Synchronization Analysis

Automated detection and categorization of audio-video synchronization issues in 2,371 MRI videos from a multispeaker speech production study.

## 🎯 Objective

Analyze large-scale MRI video datasets to identify:
- **Audio-video sync delays** (milliseconds to seconds)
- **Missing or silent audio tracks**
- **Duration mismatches** between video and audio
- **Quality degradation** issues

## 📊 Results

| Issue Category | Count | Percentage |
|---|---|---|
| GOOD_SYNC (<200ms) | 2,179 | 91.9% |
| MISSING_AUDIO | 58 | 2.4% |
| DURATION_MISMATCH | 1,524 | 64.3% |
| MINOR_DELAY (200-500ms) | 1 | 0.04% |
| **Total Analyzed** | **2,371** | **100%** |

## 🛠️ Technology Stack

| Library | Purpose |
|---------|---------|
| **OpenCV** | Video frame processing & motion detection |
| **librosa** | Audio signal processing & spectral analysis |
| **scipy.signal** | Cross-correlation for sync offset calculation |
| **pandas** | Data organization & manipulation |
| **openpyxl** | Excel report generation |
| **matplotlib/seaborn** | Data visualization |
| **ffmpeg** | Audio extraction from videos |

## 🚀 Quick Start

### Requirements
```bash
Python 3.8+
ffmpeg (for audio extraction)
```

### Installation

```bash
# Clone repository
git clone https://github.com/sejalgandhi2/MRI-Audio-Video-Sync-Analysis.git
cd MRI-Audio-Video-Sync-Analysis

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install opencv-python librosa scipy pandas openpyxl matplotlib seaborn
```

### Usage

```bash
# Navigate to scripts folder
cd Scripts/

# Update dataset path in mri_sync_analyzer.py (line ~245)
# DATASET_PATH = "/path/to/your/mri/videos"

# Run analysis
python mri_sync_analyzer.py
```

**Output files generated:**
- `Reports/MRI_Issues_Organized.xlsx` - Detailed two-sheet Excel report
- `Reports/MRI_Analysis_Charts.png` - 4-panel visualization dashboard

## 📖 How It Works

### 8-Step Pipeline

1. **VIDEO INFO** (OpenCV)
   - Extract FPS, duration, frame count

2. **EXTRACT AUDIO** (ffmpeg + librosa)
   - Extract audio streams, detect missing/silent audio

3. **AUDIO ENERGY** (librosa)
   - Compute Mel-spectrogram and energy envelope

4. **VIDEO MOTION** (OpenCV + NumPy)
   - Sample frames, calculate motion energy

5. **SYNC DETECTION** (scipy.signal - cross-correlation)
   - Correlate audio energy with video motion
   - Calculate sync offset in milliseconds

6. **CATEGORIZE** (NumPy)
   - Classify by issue type and severity

7. **REPORT** (pandas + openpyxl)
   - Generate Excel workbook with detailed results

8. **VISUALIZE** (matplotlib + seaborn)
   - Create 4-panel analysis dashboard

### Core Algorithm: Cross-Correlation Sync Detection

The key insight: **Synchronized audio-video exhibits correlated energy patterns**

```
Audio Energy Envelope + Video Motion Energy → Cross-Correlation → Sync Offset (ms)
```

- Unsupervised (no labeled training data needed)
- Works across different codecs/frame rates
- Provides quantitative millisecond-level measurements
- Results are estimates requiring manual verification

## 📁 Project Structure

```
MRI-Audio-Video-Sync-Analysis/
├── Scripts/
│   └── mri_sync_analyzer.py          # Main analysis script
├── Reports/                          # Output directory
│   ├── MRI_Issues_Organized.xlsx
│   └── MRI_Analysis_Charts.png
├── Documentation/
│   ├── PROJECT_SUMMARY.md
│   ├── VERIFICATION_GUIDE.md
│   └── METHODOLOGY_BRIEF.txt
├── Dataset_Info/
├── Visualizations/
└── README.md
```

## 📋 Methodology Brief

See [METHODOLOGY_BRIEF.txt](Documentation/METHODOLOGY_BRIEF.txt) for step-by-step explanation of each library and its role.

## ⚠️ Important Notes

**Algorithm Accuracy:**
- Results are **estimates based on cross-correlation**, not ground truth
- Requires **manual verification** for confirmation
- Use as a **screening tool**, not final authority
- Works best for videos with clear motion and audio variation

**Limitations:**
- Assumes correlated audio-motion patterns
- Fails for silent/minimal-motion scenes
- Cross-correlation has inherent mathematical limitations
- May struggle with very low quality audio

## ✅ Verification

Before using results in production, follow the [VERIFICATION_GUIDE.md](Documentation/VERIFICATION_GUIDE.md):

1. Spot-check MISSING_AUDIO files (58 files)
2. Sample high-delay categories
3. Verify duration mismatch interpretation
4. Calculate algorithm accuracy metrics
5. Refine if needed

## 🔄 Next Steps

- [ ] Manual verification of flagged videos
- [ ] Algorithm refinement based on findings
- [ ] Automated remediation (re-sync/re-encode)
- [ ] Integration into processing pipeline

## 📊 Example Output

**Excel Report** (`MRI_Issues_Organized.xlsx`):
- Sheet 1: "FILES_BY_ISSUE" - Issues organized by type
- Sheet 2: "ALL_FILES" - Complete metadata for all 2,371 videos

**Visualization** (`MRI_Analysis_Charts.png`):
- Pie chart: Issue distribution
- Histogram: Sync offset distribution
- Bar chart: Issue counts by type
- Summary statistics panel

## 🎓 Educational Value

This project demonstrates:
- Signal processing in Python (cross-correlation, spectrograms)
- Computer vision techniques (motion detection)
- Audio processing (Mel-spectrogram, energy analysis)
- Data science pipeline (from raw video to insights)
- Professional report generation
- Real-world dataset challenges

## 👥 Authors

- **Sejal Gandhi** - Lead Developer
- **Harsh Kumar** - Data Science Collaborator

## 📚 References

- Dataset: Figshare - 2D Real-time MRI Videos (Speech Production Study)
- OpenCV Docs: https://docs.opencv.org/
- librosa Docs: https://librosa.org/
- scipy.signal: https://docs.scipy.org/doc/scipy/reference/signal.html

## 📝 License

This project is open source. Feel free to use, modify, and distribute.

## 🤝 Contributing

Contributions welcome! Areas for improvement:
- Alternative sync detection methods (phase alignment, feature matching)
- Confidence scoring for detections
- GUI for manual verification
- Batch processing optimization
- Multi-threaded analysis

---

**Last Updated:** August 12, 2026  
**Status:** Analysis complete, verification in progress  
**Dataset:** 2,371 MRI videos analyzed
