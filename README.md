# Urban Flooding and Population Exposure Analysis in Jakarta
### BSCS23095_UFPEAJ_FMS

**Author:** Fouz Ul Azeem  
**Roll Number:** BSCS23095  
**Course:** Spatial Data Science  

---

## Project Overview

This project performs a comprehensive spatial analysis of flood vulnerability across Jakarta's 42 sub-districts (kecamatan). A Multi-Criteria Evaluation (MCE) framework integrates five geospatial indicators — elevation, flood hazard index, historical flood incidents (2016–2020), population density, and river proximity — into a weighted composite flood risk score. Spatial autocorrelation methods, spatial regression models, kernel density estimation, and infrastructure gap analysis are then applied to reveal the spatial structure of flood hazard and produce evidence-based policy recommendations.

---

## Folder Structure

```
BSCS23095_UFPEAJ_FMS/
│
├── bscs23095-JFA.ipynb        ← Main analysis notebook (run this)
├── README.md                           ← This file
├── abstract.pdf                        ← Project abstract
├── poster.pptx                         ← Poster (PowerPoint format)
├── poster.pdf                          ← Poster (PDF format)
│
└── data/
    ├── jakarta_districts.geojson           ← Cleaned kecamatan boundaries
    ├── jakarta_elevation_merged.tif        ← Merged SRTM elevation raster
    ├── pop.tif                             ← WorldPop population raster
    ├── flood_hazard_2023_kecamatan.csv     ← Flood hazard index by kecamatan
    ├── flood_multiyear_kecamatan.csv       ← Multi-year flood incidents (2016–2020)
    ├── district_river_distance.csv         ← Mean river distance per kecamatan
    ├── distance_to_rivers.npy              ← River distance raster array
    └── jakarta_drainage_network.geojson    ← OSM drainage network (rivers, canals, drains)
```

---

## How to Run

### Step 1: Install Required Libraries

Run the following command in your terminal or Anaconda prompt to install the exact versions used in this project:

```bash
pip install osmnx==2.1.0 geopandas==1.1.2 rasterio==1.5.0 rasterstats==0.20.0 libpysal==4.14.1 esda==2.8.1 spreg==1.8.5 splot==1.1.7 scipy==1.17.0 numpy==2.4.2 pandas==3.0.1 matplotlib==3.10.8 shapely==2.1.2 jenkspy
```

> **Note:** Using the exact versions above is strongly recommended to avoid dependency conflicts.
> Or just run:
```bash
pip install requirements.txt
```

### Step 2: Arrange the Folder

Place the notebook and the `data/` folder in the same directory exactly as shown in the folder structure above. **No path changes are needed** — all paths are set automatically relative to the notebook's location.

### Step 3: Run the Analysis Notebook

Open `bscs23095-JFA.ipynb` in Jupyter and select:

```
Kernel → Restart & Run All
```

All maps and outputs will be generated and saved automatically to the same directory as the notebook.

---

## Libraries Used

The following libraries are used in this project beyond what was covered in class:

| Library       | Version  | Purpose                                                        | Install Command                      |
|---------------|----------|----------------------------------------------------------------|--------------------------------------|
| `osmnx`       | 2.1.0    | Download administrative boundaries and features from OpenStreetMap | `pip install osmnx==2.1.0`       |
| `geopandas`   | 1.1.2    | Spatial vector data manipulation and analysis                  | `pip install geopandas==1.1.2`       |
| `rasterio`    | 1.5.0    | Raster data reading, clipping, reprojection, and masking       | `pip install rasterio==1.5.0`        |
| `rasterstats` | 0.20.0   | Compute zonal statistics from raster files per district polygon | `pip install rasterstats==0.20.0`   |
| `libpysal`    | 4.14.1   | Spatial weights matrix construction (Queen contiguity)         | `pip install libpysal==4.14.1`       |
| `esda`        | 2.8.1    | Spatial autocorrelation — Moran's I, LISA, Bivariate LISA, Gi* | `pip install esda==2.8.1`           |
| `spreg`       | 1.8.5    | Spatial regression — OLS with diagnostics, ML Spatial Lag      | `pip install spreg==1.8.5`           |
| `splot`       | 1.1.7    | Spatial statistics visualisation (LISA plots)                  | `pip install splot==1.1.7`           |
| `scipy`       | 1.17.0   | Kernel Density Estimation (KDE) for flood incident mapping     | `pip install scipy==1.17.0`          |
| `numpy`       | 2.4.2    | Numerical array operations and raster processing               | `pip install numpy==2.4.2`           |
| `pandas`      | 3.0.1    | Tabular data loading and manipulation                          | `pip install pandas==3.0.1`          |
| `matplotlib`  | 3.10.8   | Map and chart visualisation                                    | `pip install matplotlib==3.10.8`     |
| `shapely`     | 2.1.2    | Geometric operations (nearest points, unions)                  | `pip install shapely==2.1.2`         |

---

## Data Sources

| Dataset                        | Source                        | Link                                  |
|--------------------------------|-------------------------------|---------------------------------------|
| SRTM Elevation Raster          | NASA EarthExplorer            | https://earthexplorer.usgs.gov        |
| Population Density Raster      | WorldPop                      | https://www.worldpop.org              |
| Flood Hazard Index 2023        | DKI Jakarta Open Data Portal  | https://satudata.jakarta.go.id        |
| Flood Incident Records 2016–2020 | DKI Jakarta Open Data Portal | https://satudata.jakarta.go.id        |
| District Boundaries            | OpenStreetMap via OSMnx       | https://www.openstreetmap.org         |
| Drainage Network               | OpenStreetMap via Overpass API | https://www.openstreetmap.org        |

---

## Analysis Sections

The main analysis notebook is structured as follows:

1. **Library Imports** — All dependencies imported in one place
2. **Path Configuration** — All file paths defined relative to the notebook location
3. **Data Loading** — Pre-processed files loaded from the `data/` folder
4. **Preprocessing** — Raster alignment, zonal statistics, data merging, boundary clipping
5. **Multi-Criteria Evaluation (MCE)** — Scoring, weighting, composite risk classification
6. **Spatial Weights Matrix** — Queen contiguity matrix construction
7. **Global Moran's I** — Global spatial autocorrelation test
8. **Local Moran's I (LISA)** — Local cluster and outlier detection
9. **OLS Regression** — Baseline regression with spatial diagnostics
10. **ML Spatial Lag Model** — Spatially corrected regression model
11. **Getis-Ord Gi* Hotspot Analysis** — Regional hotspot and coldspot detection
12. **Kernel Density Estimation (KDE)** — Historical flood incident concentration
13. **Drainage Infrastructure Analysis** — Drainage density and investment priority mapping
14. **Bivariate LISA** — Flood risk vs. population exposure co-clustering
15. **Emergency Shelter Placement** — Spatial neighbour-based shelter recommendations

---

## Notes

- Python **3.9 or higher** is recommended.
- The analysis notebook requires **no manual path changes** — simply place the `data/` folder alongside the notebook and run.
- All output maps (Gi* map, KDE map, drainage map, shelter maps, LISA map) are saved automatically as `.png` files in the same directory as the notebook.
