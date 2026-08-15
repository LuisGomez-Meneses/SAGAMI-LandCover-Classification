# SAGAMI Land Cover Classification

Land cover classification using **Sentinel-1 and Sentinel-2 imagery and Random Forest** in the SAGAMI study area, located in **Puerto López, Meta, Colombia**.

This repository contains the data, Python source code, and classification results associated with a land cover mapping study based on the integration of multispectral Sentinel-2 imagery, Sentinel-1 Synthetic Aperture Radar (SAR) data, and reference land cover information.

---

## Study Area

The study was conducted in the **SAGAMI property**, located in the municipality of **Puerto López, Meta, Colombia**, within the Colombian Orinoquía region.

The study area contains a heterogeneous landscape including natural forest, commercial forest plantations, agricultural areas, pastures, water bodies, and infrastructure. This spatial heterogeneity provides an appropriate scenario for evaluating the ability of multisensor satellite information to discriminate different land cover types at the property scale.

<p align="center">
  <img src="Images/Figura1_zona_de_estudio.png" width="750">
</p>

<p align="center">
  <b>Figure 1.</b> Geographic location of the SAGAMI study area in Puerto López, Meta, Colombia.
</p>

---

## Data Sources

Three main sources of information were integrated:

* **Ground Truth:** reference land cover polygons representing the classes identified within the SAGAMI study area.
* **Sentinel-2:** multispectral optical observations used to characterize the spectral properties of the land cover classes.
* **Sentinel-1:** SAR observations using VV and VH polarizations, providing complementary information related to surface and vegetation structure.

Sentinel-1 and Sentinel-2 observations from **2025** were processed to generate representative annual composites.

All spatial information used for dataset construction was harmonized at a spatial resolution of **10 m**.

---

## Dataset Construction

The Ground Truth and satellite products were spatially integrated to construct a structured dataset suitable for supervised machine learning.

For every valid Ground Truth pixel, the corresponding Sentinel-2 spectral information and Sentinel-1 radar backscatter values were extracted. Consequently, each row of the resulting dataset represents a spatial observation associated with a unique land cover class.

<p align="center">
  <img src="Images/Imagen4.png" width="950">
</p>

<p align="center">
  <b>Figure 2.</b> Pixel-level integration of Ground Truth, Sentinel-2, and Sentinel-1 information for construction of the structured land cover classification dataset.
</p>

The resulting dataset follows the general structure:

```text
Pixel_ID | X | Y | VV | VH | Sentinel-2 bands | Class
```

This representation allows the geospatial information to be transformed into a tabular dataset suitable for training and evaluating the Random Forest classifier.

---

## Land Cover Classification

A **Random Forest (RF)** classifier was used to discriminate the land cover types present within the SAGAMI study area.

The final classification scheme contains the following classes:

| Class                 |
| --------------------- |
| Natural forest        |
| Rice crop             |
| Eucalyptus plantation |
| Lagoon                |
| Mixed plantation      |
| Pine plantation       |
| Pasture               |
| River                 |
| Simarouba plantation  |
| Infrastructure        |

The predictor variables correspond to the multispectral information derived from Sentinel-2 and the VV and VH radar polarizations obtained from Sentinel-1.

---

## Model Evaluation

Model performance was evaluated using an independent subset of the structured dataset.

The evaluation included class-specific performance metrics and analysis of the confusion matrix to identify both correctly classified observations and the principal sources of confusion between land cover classes.

<p align="center">
  <img src="Images/Matriz%20Actualizada.png" width="850">
</p>

<p align="center">
  <b>Figure 3.</b> Normalized confusion matrix obtained for the Random Forest land cover classification model.
</p>

The confusion matrix shows high classification performance for several classes. **Natural forest, rice crop, and lagoon** reached normalized diagonal values of **0.959, 0.953, and 0.979**, respectively.

The main classification errors occurred among forest plantation categories. In particular, mixed plantations showed confusion with pine plantations, while eucalyptus plantations also presented confusion with pine and infrastructure. These patterns reflect the greater difficulty of separating land covers with similar spectral and structural characteristics.

---

## Repository Structure

```text
SAGAMI-LandCover-Classification/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── src/
│
├── results/
│
├── Images/
│   ├── Figura1_zona_de_estudio.png
│   ├── Imagen4.png
│   └── Matriz Actualizada.png
│
└── README.md
```

### `data/raw`

Original input information used as the starting point for Ground Truth construction.

### `data/processed`

Processed spatial information and structured datasets generated through the integration of Ground Truth, Sentinel-1, and Sentinel-2 information.

### `src`

Python scripts used for data preparation, dataset construction, Random Forest training, and model evaluation.

### `results`

Outputs generated by the classification experiments, including evaluation metrics, confusion matrices, and variable importance results.

### `Images`

Figures used to document the study area, dataset construction methodology, and classification results.

---

## Workflow

The general processing workflow implemented in this repository is:

**Ground Truth → Sentinel-1 & Sentinel-2 integration → Pixel-level dataset → Random Forest → Model evaluation**

This organization allows the different stages of the experiment to be traced from the original reference information to the final classification results.

---

## Reproducibility

The objective of this repository is to provide the data products, processing scripts, and model outputs necessary to document and reproduce the main experiments presented in the associated research article.

The complete Sentinel-1 and Sentinel-2 image collections are not stored directly in this repository due to their size. Instead, the repository documents the processing workflow and provides the derived datasets used for model development and evaluation.

---

## Citation

If you use the data or source code available in this repository, please cite the associated research article.

Citation information will be added once the associated article is published.

---


Additional co-authors and institutional affiliations will be added according to the final version of the associated article.
