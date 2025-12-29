# RSE-EPI-Transport-Corridor-Assessment
Remote Sensing Engineering Performance Index (RSE-EPI) for corridor resilience, early-warning &amp; threshold intervention.
# Remote Sensing Engineering Performance Index (RSE-EPI)
**Author:** Sitenda Amos (AugustKizito)  
**Application:** Tanzania SGR, Central & Mtwara Corridors  
**Keywords:** NDVI, MNDWI, VIIRS NTL, SDM, Spillover, Early-Warning, EO-based Engineering

This repository contains code, sample data, and workflow documentation for the RSE-EPI
Remote Sensing Performance Dashboard developed for multimodal transport corridors.
It supports reproducibility, open-science compliance, and Zenodo archiving.

---

## 📂 Repository Structure
- `/data` – Sample datasets + access instructions  
- `/src` – Processing scripts (NDVI, MNDWI, NTL, SDM structure)  
- `/outputs` – Figures & tables used in the manuscript  
- `/docs` – Supplementary files, report notes, appendices  

---

## 🔗 DOI & Archival Information
A permanent DOI will be generated through Zenodo once the first release is published.
**(Placeholder until you publish release)**  
> DOI: _pending (to be updated after Zenodo release)_

---

## 🛰️ Data Access Sources
- Sentinel-2: https://dataspace.copernicus.eu/
- VIIRS NTL: https://ladsweb.modaps.eosdis.nasa.gov/
- SRTM DEM: https://earthexplorer.usgs.gov/

---

## 📜 License
Released under the **MIT License** to enable reuse.

---patial Analysis Pipeline for RSE-EPI Engineering Threshold Framework
Author: AugustKizito (2025)

Purpose:
- Extract NDVI, MNDWI, NTL, and slope metrics
- Classify engineering thresholds (stable/at-risk/critical)
- Export analysis for SDM model fitting and mapping
"""

import geopandas as gpd
import rasterio
import numpy as np
import pandas as pd

# --- Load Corridor Buffer Zones ---
corridors = gpd.read_file("../data/processed/corridor_buffers_15km_50km.shp")

# --- Load NDVI / MNDWI raster files ---
ndvi = rasterio.open("../data/processed/NDVI_zscore.tif")
mndwi = rasterio.open("../data/processed/MNDWI.tif")

# Example threshold rule:
def classify_threshold(ndvi_val, mndwi_val):
    if ndvi_val < -0.8 and mndwi_val < 0.10:
        return "Critical"
    elif ndvi_val < -0.8 or mndwi_val < 0.10:
        return "At-Risk"
    else:
        return "Stable"

print("Pipeline ready. Run SDM model in SDM_m
# Spatial Durbin Model (SDM) for RSE-EPI Propagation
# Author: AugustKizito (2025)

library(spdep)
library(spatialreg)
library(rgdal)

data <- read.csv("../data/processed/RSE_EPI_model_data.csv")

# Spatial weights matrix
coords <- cbind(data$lon, data$lat)
W <- knn2nb(knearneigh(coords, k=6))
Wm <- nb2listw(W, style="W")

# SDM Model
sdm <- lagsarlm(RSE_EPI ~ NDVI + MNDWI + NTL + Slope, data=data, listw=Wm, type="mixed")
summary(sdm)

write.csv(summary(sdm)$Coef, "../results/tables/SDM_full_results.csv")
geopandas
rasterio
numpy
pandas
scikit-learn
matplotlib
spreg
pysal
ROCESSED ANALYSIS-READY DATA
These files were pre-processed for use in the RSE-EPI model.

Preprocessing Steps:
1. Atmospheric correction & cloud masking (Sentinel-2 SR)
2. NDVI and MNDWI extraction per corridor buffer (15km core, 50km spillover)
3. Resampling to common CRS: UTM 36S, 30m resolution
4. Feature normalization (Z-score)
5. Slope extraction from SRTM-derived DEM

Files here correspond to the data used directly in figures, tables, and model fitting.
For code implementation, see `/src/`.
RAW DATA (UNMODIFIED)
This folder contains original, source-level datasets before cleaning or processing.
Files are provided for transparency and reproducibility. These datasets were not altered.

Sources:
- Sentinel-2 MSI Vegetation Index & reflectance bands (Copernicus Open Access Hub)
- VIIRS Night-Time Lights (Earth Observation Group, NOAA)
- SRTM DEM elevation products (USGS EarthExplorer)
- Corridor shapefiles and district administrative boundaries (Tanzania National Bureau of Statistics)

Use restrictions:
All sources are open-access, but users must cite the providers if reused.
Dear Editor,

I am pleased to submit our manuscript entitled:

**"Operationalizing Remote Sensing Thresholds for Engineering Decision Support in Multimodal Transport Corridors"**

for consideration in *Remote Sensing* (Q1, MDPI).  
The study introduces a reproducible engineering workflow that converts NDVI, MNDWI, NTL, and terrain derivatives into deterministic intervention thresholds and early-warning classification (78–97 day lead-time) for Tanzania’s transport corridors.

The manuscript:
✔ aligns with the journal’s Remote Sensing–Engineering integration scope  
✔ demonstrates a validated Spatial Durbin Model (ρ = 0.417, p < 0.01)  
✔ provides a full open-science repository + data availability link  
✔ advances EO from monitoring to engineering control and governance  

There are no conflicts of interest, all datasets are open-access, and the code is made available for replication.

We believe this work offers technical and policy relevance for climate-resilient infrastructure systems and Global South corridor governance.

Sincerely,  
GitHub: https://github.com/AugustKizito/RSE-EPI-Corridor-Analysis
# RSE-EPI: Remote Sensing Engineering Performance Index  
### Threshold-Based Early Warning System for Multimodal Transport Corridors (Tanzania)

This repository contains the full open-science package for the publication:

**"Operationalizing Remote Sensing Thresholds for Engineering Decision Support in Multimodal Corridors (Tanzania Case Study)"**

## 📌 Repository Contents
| Folder | Purpose |
|--------|----------|
| data/ | Sentinel-2, VIIRS NTL, SRTM DEM, processed NDVI/MNDWI datasets |
| src/ | Python & GEE analysis scripts, SDM model code |
| results/ | Figures, tables, model outputs, diagnostics |
| manuscript/ | Final PDF, supplementary materials, cover letter |
| LICENSE | MIT open access license |

## 📍 Dataset DOI
A DOI will be minted: **Zenodo → GitHub integration planned.**
Proposed DOI placeholder: `doi:10.5281/zenodo.xxxxxxx`

## 💾 Data Availability Statement
All data and code used in this study are available in this repository under MIT License.  
EO sources: Sentinel-2 MSI, VIIRS NTL, SRTM DEM (public domain).  
Processing scripts: `src/` folder.

## 📌 Citation
If you use this repository, please cite:
**Sitenda, A., 2025. RSE-EPI Corridor Risk Diagnostics. GitHub.**
RSE-EPI-Transport-Corridor-Assessment/
│
├── data/
│   ├── sample/
│   └── README_data_access.md
│
├── src/
│   ├── preprocessing/
│   ├── sdm_model/
│   └── rse_epi_index/
│
├── outputs/
│   ├── figures/
│   └── tables/
│
├── docs/
│   ├── manuscript/
│   └── supplementary/
│
├── LICENSE
└── README.md

