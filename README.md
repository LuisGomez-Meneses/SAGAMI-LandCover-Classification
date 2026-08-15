# SAGAMI Land Cover Classification

Land cover classification using **Sentinel-1 and Sentinel-2 imagery** and a **Random Forest (RF)** classifier in the SAGAMI study area, located in **Puerto López, Meta, Colombia**.

This repository contains the datasets, source code, figures, and results associated with the land cover classification workflow developed for the SAGAMI study area. The approach integrates multispectral information from Sentinel-2 and Synthetic Aperture Radar (SAR) information from Sentinel-1 to discriminate natural vegetation, forest plantations, agricultural areas, water bodies, and infrastructure.

---

## Study Area

The study was conducted at the **SAGAMI property**, located in the municipality of Puerto López, Meta, Colombia. The area is characterized by a heterogeneous landscape composed of natural vegetation, commercial forest plantations, pastures, agricultural areas, water bodies, and infrastructure.

<p align="center">
  <img src="Images/Figura1_zona_de_estudio.png" width="750">
</p>

<p align="center">
  <b>Figure 1.</b> Location of the SAGAMI study area in Puerto López, Meta, Colombia.
</p>

---

## Data

The classification workflow integrates three main sources of information:

* **Ground Truth:** land cover polygons derived from the available cartographic information of the SAGAMI property and subsequently processed for model training and validation.
* **Sentinel-2:** multispectral optical imagery used to characterize the spectral response of the different land cover classes.
* **Sentinel-1:** Synthetic Aperture Radar (SAR) imagery using VV and VH polarizations to provide complementary information on vegetation and surface structure.

Sentinel imagery corresponding to **2025** was processed to generate representative annual composites for the study area.

The spatial information was harmonized to a common **10 m spatial resolution**, allowing the Sentinel-1 and Sentinel-2 variables to be associated with the corresponding Ground Truth class at pixel level.

---

## Methodology

The general workflow consists of:

1. Ground Truth preparation and validation.
2. Sentinel-2 image preprocessing.
3. Sentinel-1 image preprocessing.
4. Spatial harmonization of the satellite products.
5. Pixel-level extraction of Sentinel-1 and Sentinel-2 variables.
6. Construction of the structured classification dataset.
7. Random Forest model training.
8. Model evaluation using independent validation data.
9. Confusion matrix analysis.
10. Feature importance analysis.

Each observation in the final structured dataset represents a spatial pixel associated with its Sentinel-2 spectral variables, Sentinel-1 radar variables, and corresponding land cover class.

---

## Land Cover Classes

The final classification scheme comprises **10 land cover classes**:

| ID | Land Cover Class                     |
| -: | ------------------------------------ |
|  1 | Natural forest                       |
|  2 | Pine plantation                      |
|  3 | Eucalyptus plantation                |
|  4 | Simarouba plantation                 |
|  5 | Mixed plantation (pine + eucalyptus) |
|  6 | Pasture                              |
|  7 | Rice crop                            |
|  8 | River                                |
|  9 | Lagoon                               |
| 10 | Infrastructure                       |

The classification scheme was designed to represent both general land cover types and the forest plantation classes of interest within the SAGAMI property.

---

## Random Forest Classification

A **Random Forest classifier** was trained using the integrated Sentinel-1 and Sentinel-2 dataset.

The predictor variables include multispectral information from Sentinel-2 and radar backscatter information from Sentinel-1. The Ground Truth polygons were used to associate each valid pixel with its corresponding reference class.

The model performance was evaluated using class-specific and global classification metrics, including precision/User's Accuracy, recall/Producer's Accuracy, F1-score, and confusion matrices.

---

## Classification Performance

The confusion matrix provides a detailed assessment of the ability of the Random Forest model to discriminate among the different land cover classes.

<p align="center">
  <img src="Images/Matriz%20Actualizada.png" width="850">
</p>

<p align="center">
  <b>Figure 2.</b> Confusion matrix obtained for the Random Forest land cover classification model.
</p>

The results show strong discrimination for several land cover categories, particularly natural forest, rice crops, and lagoon areas. Most classification errors are concentrated among forest plantation classes, where similarities in spectral and structural characteristics can increase inter-class confusion.

---

## Feature Importance

Random Forest feature importance was analyzed to determine the relative contribution of the Sentinel-1 and Sentinel-2 variables to the classification process.

<p align="center">
  <img src="Images/Imagen4.png" width="800">
</p>

<p align="center">
  <b>Figure 3.</b> Feature importance of Sentinel-1 and Sentinel-2 variables in the Random Forest classification model.
</p>

The feature importance analysis provides insight into the contribution of optical spectral information and radar backscatter to the discrimination of the land cover classes. This analysis is particularly relevant for evaluating the complementary contribution of Sentinel-1 SAR observations to the multispectral information provided by Sentinel-2.

---

## Repository Structure

```text
SAGAMI-LandCover-Classification/
│
├── data/
│   ├── raw/                 # Original input data
│   └── processed/           # Structured and processed datasets
│
├── src/                     # Python source code
│
├── results/                 # Model outputs and evaluation results
│
├── Images/                  # Figures used in the study
│
├── README.md
├── requirements.txt
└── LICENSE
```

### `data/raw`

Contains the original spatial information used as input for Ground Truth construction, when redistribution of the source data is permitted.

### `data/processed`

Contains the processed Ground Truth and structured datasets generated from the integration of Sentinel-1, Sentinel-2, and reference land cover information.

### `src`

Contains the Python scripts required for Ground Truth processing, satellite data preparation, dataset generation, Random Forest training, and model evaluation.

### `results`

Contains the classification metrics, confusion matrices, feature importance values, and other outputs generated during model evaluation.

### `Images`

Contains the figures associated with the study and used to summarize the study area and principal classification results.

---

## Reproducibility

The repository is organized to reproduce the main processing sequence:

**Original cartography → Ground Truth → Sentinel-1/Sentinel-2 integration → Structured dataset → Random Forest → Classification evaluation**

The processed dataset and source code provided in this repository are intended to facilitate the reproduction and verification of the classification experiments reported in the associated research work.

---

## Satellite Data

Sentinel-1 and Sentinel-2 imagery are part of the **Copernicus Earth Observation Programme** of the European Union and were used as the primary Earth observation data sources for this study.

Due to the size of the original satellite imagery, the complete Sentinel image archive is not stored directly in this GitHub repository. Instead, the repository provides the processed information and source code required to document and reproduce the analytical workflow.

---

## Citation

If you use this repository, dataset, or source code in academic work, please cite the associated research article.

> Citation information will be added after publication of the associated article.

---

## License

The source code and data licensing conditions will be specified according to the redistribution permissions of the original and derived datasets.
