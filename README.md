# Genetic encoding and mutagenesis of RNA droplet phenotypes – analysis code

This repository contains analysis notebooks used to quantify RNA droplet phenotypes from microscopy data, from the corresponding pre-print: _https://chemrxiv.org/engage/chemrxiv/article-details/680ca3e6927d1c2e66de8256_. 
The workflows include segmentation of RNA droplets, quantification of droplet and vacuole (hole) areas, and analysis of droplet dynamics from TrackMate tracking data.

---

## Contents

### 1. `Droplets_detection.ipynb`

Segmentation and feature extraction for RNA droplets and their internal holes.

**Main tasks:**

- Load microscopy images (`.tif` or `.czi`).
- Segment droplets and internal vacuoles.
- Measure droplet properties with `skimage.measure.regionprops`, including:
  - `area`, `area_filled`, `hollow area` (vacuole area),
  - `axis_major_length`, `axis_minor_length`, `perimeter`,
  - mean fluorescence intensity,
  - metadata: `pixel size`, `time`, `condition`, `image_ID`, `replicate`, `field`.
- Compute derived metrics such as:
  - vacuole-to-droplet area ratio (`area ratios`),
  - conversion from pixels to µm / µm².
- Save all measurements to a `.csv` file for downstream analysis.

You typically run this notebook **once per condition / dataset** to generate segmentation outputs.

---

### 2. `Droplet_size_quantification.ipynb`

Analysis and plotting of the segmentation results produced by `Droplets_detection.ipynb`.

**Main tasks:**

- Load one or several CSV files exported from `Droplets_detection.ipynb`.
- Convert pixel-based measurements to physical units (µm and µm²) using `pixel size` and `pixel area`.
- Combine replicates and conditions into a single `pandas` DataFrame.
- Generate summary plots for:
  - droplet size distributions,
  - vacuole (hollow) area and area fractions,
  - time-lapse evolution of droplet and vacuole sizes across conditions.
- Perform statistical comparisons.
Use this notebook to produce the figures and statistics for droplet and vacuole size.

---

### 3. 'tracking_movement'

Processing and plotting of droplet trajectories exported from TrackMate (ImageJ/Fiji).

**Main tasks:**

- Read TrackMate `.xml` files via `xml.etree.ElementTree`.
- Extract trajectory information for individual droplets over time.
- Compute motility descriptors such as mean squared displacement (MSD).
- Select and analyse “top” trajectories based on simple criteria (e.g. track length).
- Plot:
  - MSD curves,
  - summary statistics (e.g. violin plots per condition and statistical tests).

### 4. For code related to the theory and phase separation diagram please visit: "https://git.rz.uni-augsburg.de/jaiswapr/RNA_Nanostar"


---
