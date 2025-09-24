
## Project Overview

This project automates the process of:

1. Reading raw **train videos**.
2. **Extracting frames** at fixed intervals (e.g., every 30th frame).
3. Saving those frames into structured folders.
4. Generating a **PDF summary report** with selected thumbnails for each video.
5. Zipping and exporting all results for easy download.

It is designed to run on **Google Colab** with **Google Drive integration**.

---

## Tech Stack

* **Python 3 (Google Colab)**
* **Libraries Used**:

  * OpenCV → Frame extraction
  * MoviePy → Video handling
  * ReportLab → PDF report generation
  * NumPy & SciPy → Data utilities
  * gdown → Google Drive dataset download

---

## Folder Structure

```
├── Raw_video/                 # Input videos (.mp4 files)
├── Processed/                 # Output folder (auto-created)
│   ├── <video_name>/          # Per input video
│   │   ├── frame_xxxxxx.jpg   # Extracted frames
│   │   └── Report_<video>.pdf # PDF summary for that video
├── Processed_Output.zip       # Final zipped results
└── README.md
```

---

##  How to Run

### 1️ Clone & Open in Google Colab

Upload your code files + notebook to **Colab** and connect to Google Drive.

```python
from google.colab import drive
drive.mount('/content/drive')
```

---

### 2️ Install Dependencies

```python
!pip install opencv-python-headless moviepy ultralytics reportlab scipy gdown
```

---

### 3️ Download Input Videos from Google Drive

```python
!gdown --folder https://drive.google.com/drive/folders/<your-folder-id>
```

Your videos will be stored in `/content/Raw_video`.

---

### 4️ Run Processing Pipeline

```python
# Extract frames + generate PDF reports
videos = [f for f in os.listdir(RAW_DIR) if f.lower().endswith(".mp4")]
for v in videos:
    vpath = os.path.join(RAW_DIR, v)
    vname = Path(v).stem
    out_folder = os.path.join(OUTPUT_DIR, vname)
    os.makedirs(out_folder, exist_ok=True)

    frames = extract_frames(vpath, out_folder, step=FRAME_EVERY)
    pdf_path = os.path.join(out_folder, f"Report_{vname}.pdf")
    make_pdf(pdf_path, vname, frames)
```

---

### 5️ Export All Results

```python
import shutil
from google.colab import files

shutil.make_archive("/content/Processed_Output", 'zip', "/content/Processed")
files.download("/content/Processed_Output.zip")
```


## Features

✅ Extract frames at fixed intervals
✅ Auto-generate structured PDF report per video
✅ Works with multiple input videos
✅ One-click ZIP + download of all outputs
✅ Fully integrated with Google Drive

---

## Limitations

* Frame extraction is **fixed step** (every N frames).
* Reports currently show only **6 sample frames per video**.
* Works best on **.mp4 videos** with clear train visuals.

---

## Author

**Anirudha Kolay**

* AI/ML & Data Analytics Engineer
* Passionate about Computer Vision & Video Analytics
* [LinkedIn](www.linkedin.com/in/anirudhakolay) | [GitHub](https://github.com/anirudhakolay)

---

👉 Do you want me to also **add usage screenshots (like sample PDF output)** section in the README so your GitHub page looks more visual and professional?
