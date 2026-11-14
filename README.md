# Crack Detection and Assessment Using Computer Vision Intelligence

Crack detection and assessment on concrete surfaces using classical computer vision.
Phase 1 benchmarks classical feature descriptors (HOG, GLOH, SURF, BRISK, MSER, Shi-Tomasi)
with SVM, Random Forest, XGBoost and Decision Tree classifiers on SDNET2018. Phase 2 works on
UAV-GCD crack annotations, and an edge and Hough-transform pipeline is included.

M.Tech project, Amrita School of Computing, Coimbatore.

- **Student:** Janarthana Prabu S (CB.SC.P2AIE25007)
- **Guide:** Dr. Padmavathi S

**Documentation portal:** https://janarthanaprabu.github.io/Crack-Detection-and-Assessment-Using-Computer-Vision-Intelligence/
(objectives, problem statement, methodology, results, literature survey and notebook outputs)

---

## What is in this repository

```
.
├── data/
│   ├── Benchmark_Results.xlsx        accuracy, precision, recall, F1 per feature and classifier
│   └── Literature_Survey.xlsx        17-paper literature survey
├── docs/                             documentation portal (published with GitHub Pages)
├── notebooks/
│   ├── Edge_detction_applied_Hough_Transform.ipynb   Phase 2, edge detection and Hough transform
│   ├── crack-detection-sdnet-2018.ipynb              Phase 1, grid-based (patch) descriptors
│   ├── gloh-crack-detection.ipynb                    Phase 1, GLOH (128-D)
│   ├── jsonfile_UAV_Dataset.ipynb                    Phase 2, UAV-GCD images with JSON annotations
│   └── without-patch.ipynb                           Phase 1, patch-free (global) descriptors
├── .gitignore                        files Git should not track
├── INSTALL.md                        installation and run guide
├── README.md                         this file
└── requirements.txt                  Python packages
```

## Notebooks

| Notebook | What it does |
|---|---|
| `crack-detection-sdnet-2018.ipynb` | Grid-based feature vectors on SDNET2018: Combined Vector (205-D), Spatial HOG, Shi-Tomasi, MSER, Spatial SURF and patch-based BRISK. Each is evaluated with four classifiers on 2-class (crack / no crack), 3-class (deck / wall / pavement) and 6-class tasks. |
| `without-patch.ipynb` | The same evaluation using global (patch-free) Shi-Tomasi, MSER, SURF and BRISK features. |
| `gloh-crack-detection.ipynb` | GLOH (128-D log-polar gradient histogram). It contains two runs: the main run, and a second run that also reports balanced accuracy and macro F1. |
| `jsonfile_UAV_Dataset.ipynb` | Loads UAV-GCD images together with their JSON annotations (Google Colab). |
| `Edge_detction_applied_Hough_Transform.ipynb` | Edge detection and Hough line transform on road and crack images, with histograms of edge pixels per bin (Google Colab). Outputs are cleared in this repository because the file is very large. |

## Datasets

- **SDNET2018** (56,092 images of 256 x 256 pixels: bridge decks, walls and pavements, cracked and uncracked).
  Original authors: S. Dorafshan, R. J. Thomas and M. Maguire, "SDNET2018: An annotated image dataset for
  non-contact concrete crack detection using deep convolutional neural networks," *Data in Brief*, vol. 21,
  pp. 1664-1668, 2018.
  Kaggle copy used in the notebooks: A. Sharma, "SDNET2018: Structural Defects Network (Concrete Crack Images Dataset)," Kaggle:
  https://www.kaggle.com/datasets/aniruddhsharma/structural-defects-network-concrete-crack-images
  The dataset has its own licence. It is not included in this repository.
- **UAV-GCD:** UAV-captured crack images with JSON annotations, used in Phase 2. It is not included in this repository.

## How to run

See [INSTALL.md](INSTALL.md). The easiest way is to run the notebooks on Kaggle with the SDNET2018 dataset added as input.

## Reproducibility notes

- **Random image sampling.** Each notebook picks a fixed number of images per class (for example 2,000) after a seeded shuffle of the file list.
  The order of that list can differ between environments, so numbers can change by about 1-2 percentage points between runs. The saved outputs in each notebook come from the run stored in that notebook. The Spatial HOG values in `data/Benchmark_Results.xlsx` differ slightly from the Spatial HOG outputs saved in the notebook (see the next note).
- **Two Spatial HOG variants.** `crack-detection-sdnet-2018.ipynb` contains a 345-D vector (HOG plus gradient statistics) and a 320-D HOG-only vector. The headings in the notebook say which is which.
- **SURF.** SURF needs an OpenCV build that includes the non-free modules. If SURF is not available, the notebooks automatically fall back to FAST keypoints with SIFT or ORB descriptors.
- **Model files.** Running the GLOH notebook creates `model_gloh_2c.pkl`, `label_encoder_2c.pkl` and `kmeans_codebook.pkl`. These are not stored in the repository.

## Author

Janarthana Prabu S, M.Tech, Amrita School of Computing, Coimbatore.
Guide: Dr. Padmavathi S.
