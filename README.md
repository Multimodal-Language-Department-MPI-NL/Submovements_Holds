# Submovements and Holds

Detection of holds and submovements from Mediapipe time series.

## Inputs
`data/processed/timeseries/*.csv` with axis-suffixed columns like `WRIST_x, WRIST_y, WRIST_z`.  
Optional time column in seconds. If missing, set `--fs`.

## Environment
conda env create -f environment.yml
conda activate submovements

## CLI
# run hold detection and submovement peak picking on a file
python scripts/detect_holds.py \
  --in data/processed/timeseries/1295_LG_past_layout1_body.csv \
  --out results/segments/1295_LG_segments.csv \
  --fs 30 --thresh 0.01 --min-dur 0.2 --merge-gap 0.1 --min-ipi 0.1

## Notebook
jupyter lab
# open notebooks/01-gesture_hold_time_pauses.ipynb

## Outputs
`results/segments/*.csv` with rows for `hold` and `submovement` events.