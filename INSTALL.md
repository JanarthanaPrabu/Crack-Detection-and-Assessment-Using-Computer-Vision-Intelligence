# Installation and run guide

There are three ways to run the notebooks. Option A is the easiest and is the setup the project was run in.

## Option A: Kaggle (recommended for the SDNET2018 notebooks)

1. Create a free account on https://www.kaggle.com and verify your phone number (needed for GPU and internet).
2. Click **Create, then New Notebook**, then **File, then Import Notebook**, and upload one of these from the `notebooks/` folder:
   `crack-detection-sdnet-2018.ipynb`, `without-patch.ipynb` or `gloh-crack-detection.ipynb`.
3. In the right panel click **Add Input** and search for **"Structural Defects Network (SDNET) 2018"**
   (https://www.kaggle.com/datasets/aniruddhsharma/structural-defects-network-concrete-crack-images). Add it.
4. Click **Run All**. The notebooks read images from `/kaggle/input`, so no path changes are needed.
5. A GPU is not required. It is only used by the optional BRISK cell, and only if RAPIDS cuML is available.

Run time depends on the notebook. Some cells take 5 to 15 minutes because they extract features from all 56,092 images.

## Option B: Run on your own computer

Requirements: Python 3.10 or newer.

```bash
# 1. Get the code
git clone https://github.com/JanarthanaPrabu/Crack-Detection-and-Assessment-Using-Computer-Vision-Intelligence.git
cd Crack-Detection-and-Assessment-Using-Computer-Vision-Intelligence

# 2. Create a virtual environment
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate

# 3. Install the packages
pip install -r requirements.txt

# 4. Start Jupyter
jupyter notebook
```

Then:

1. Download SDNET2018 from the Kaggle link above and unzip it into `data/SDNET2018/`.
2. In each notebook, find the line `os.walk('/kaggle/input')` and change `'/kaggle/input'` to `'data/SDNET2018'`.
3. Open a notebook from `notebooks/` and choose **Run All**.

If SURF gives an error, install `opencv-contrib-python` (not plain `opencv-python`). If your OpenCV build still has no SURF, the notebook falls back to FAST with SIFT or ORB automatically.

## Option C: Google Colab (for the UAV and Hough notebooks)

`jsonfile_UAV_Dataset.ipynb` and `Edge_detction_applied_Hough_Transform.ipynb` were written for Google Colab and use `google.colab.files.upload()`.

1. Open https://colab.research.google.com and choose **File, then Upload notebook**.
2. Run the cells in order. When a cell asks you to upload files, select the image (`.jpg` or `.png`) and the matching annotation (`.json`) files from your UAV-GCD data.

## Common problems

| Problem | Fix |
|---|---|
| `ModuleNotFoundError` | Run `pip install -r requirements.txt` again inside the virtual environment. |
| `cv2.xfeatures2d` has no attribute `SURF_create` | Install `opencv-contrib-python`, or ignore it. The notebook falls back to another descriptor. |
| Accuracy differs by 1 to 2 points from the saved outputs | This is expected. The image sample depends on file order, see the README. |
| "Expected both 'Crack' and 'No Crack' images" | The dataset path is wrong or only part of SDNET2018 was loaded. Check the input path. |
| Widget or upload button does not appear | It only works in Kaggle or Colab. Skip that cell, since it is a demo of the trained model. |
