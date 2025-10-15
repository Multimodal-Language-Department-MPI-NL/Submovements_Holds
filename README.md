# Submovements and Holds

> Attribution: Use the script prepared for the focus group session. Attribute to this Envision Box module: [Module](https://www.envisionbox.org/embedded_MergingMultimodal_inPython.html)

Detect holds and submovements from MediaPipe keypoint time series and summarize gesture pauses.

## 🔬 Research Context

This module shows how to calculate the number of submovements of a movement signal based on peak speed and detect movement holds (i.e., pauses) below a certain speed threshold. These measures relate to how complex and/or segmented a movement signal is.

## 🎯 What This Project Does

1. **Load keypoints**: Read body landmark time series
2. **Convert to OpenPose-like format**: Map selected MediaPipe landmarks to expected keys
3. **Detect submovements**: Peak picking on smoothed hand velocity traces
4. **Detect holds**: Identify low-velocity clusters and compute durations
5. **Batch processing**: Optionally compute measures across multiple files

## 📊 Smoothing Process

1. **Begin with Cleaned Data**: Use processed time series with `time` and landmark coordinates
2. **Convert Coordinates**: Build OpenPose-like columns (e.g., `L_Hand`, `R_Hand`, `Neck`, `MidHip`)
3. **Tune Parameters**: Interactively set `height`, `prominence`, `distance` for peak detection
4. **Compute Metrics**: Submovement counts; number of holds, total/average hold duration
5. **Export**: Save per-file summaries to CSV

## 🔧 Smoothing Techniques

- **Velocity estimation**: Frame-to-frame displacement × FPS
- **Smoothing**: Savitzky–Golay on velocity before peak picking
- **Peak detection**: `scipy.signal.find_peaks` with `height`, `prominence`, `distance`
- **Hold detection**: Velocity thresholding and clustering into contiguous segments

## 📁 Project Structure

```
Submovements_Holds/
├── README.md
├── environment.yml
├── notebooks/
│   └── 01-gesture_hold_time_pauses.ipynb
├── data/
│   └── processed/
│       └── timeseries/                 # Input CSVs
├── results/
│   ├── segments/                       # Output event segments (optional)
│   └── figures/
│       └── diagram.png
└── scripts/
    └── detect_holds.py                 # (If used)
```

## 🚀 Quick Start

### Prerequisites

```bash
conda env create -f environment.yml
conda activate submovements
```

### Run the Interactive Notebook

```bash
jupyter lab
# Open notebooks/01-gesture_hold_time_pauses.ipynb
```


## 📈 Data Format

### Input
- **CSV files**: Landmark coordinates per frame; include `time` if available

### Output
- **CSV summaries**: Per-file metrics (e.g., `num_holds`, `avg_hold_duration`)
- **Interactive figures**: Peak locations, hold intervals overlaid on velocity

## 🔗 Related Projects

- `https://github.com/Multimodal-Language-Department-MPI-NL/Smoothing`
- `https://github.com/Multimodal-Language-Department-MPI-NL/Normalization`
- `https://github.com/Multimodal-Language-Department-MPI-NL/Speed_Acceleration_Jerk`

## 📖 References

- **Attribution**: Envision Box Module
- `scipy.signal.find_peaks` documentation