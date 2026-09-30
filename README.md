# ECG R-peak Analysis — MIT-BIH Record 100

An exploratory biomedical signal-processing project adapted from my coursework notebook. It loads one ECG channel from record 100 of the MIT-BIH Arrhythmia Database, adds simulated baseline wander, filters the signal, identifies candidate R-peaks, and estimates the average heart rate from RR intervals.

## Run it

```bash
python -m venv .venv
# Activate the virtual environment, then:
pip install -r requirements.txt
jupyter notebook ecg_rpeak_analysis.ipynb
```

Run the cells from top to bottom. The first run downloads record 100 and `atr` annotations to `data/mitdb/`; an internet connection is required. That folder is excluded from Git. You can also upload the notebook to Google Colab, install the packages from `requirements.txt` in its first code cell, and run it there.

## Workflow

1. Load record 100's first ECG channel and sampling rate.
2. Add a simulated 0.1 Hz baseline wander (0.4 mV amplitude).
3. Apply a 5–15 Hz Butterworth band-pass, derivative, squaring, and 150 ms moving average.
4. Find candidate peaks, visualize the first 10 seconds, and compute `60 / mean(RR intervals)` in bpm.

The notebook loads reference annotations but does not evaluate detections against them. The threshold is heuristic. This is a learning project, **not a validated detector, diagnosis, or clinical tool**. No numerical accuracy claim is made. The original coursework notebook had repeated exploratory cells and a cell-order error; this version consolidates the workflow for sequential execution.

## Data and citation

Dataset: [MIT-BIH Arrhythmia Database v1.0.0 on PhysioNet](https://physionet.org/content/mitdb/1.0.0/) (record 100). The data are distributed by PhysioNet under the Open Data Commons Attribution License v1.0 and are downloaded directly when the notebook runs.

Moody GB, Mark RG. “The impact of the MIT-BIH Arrhythmia Database.” *IEEE Engineering in Medicine and Biology Magazine* 20(3):45–50, 2001.
