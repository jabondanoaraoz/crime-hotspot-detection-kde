# Chicago Crime Hotspot Analysis: A KDE Approach

Geospatial analysis of **17,747 crime incidents** (robberies and homicides) recorded in Chicago during summer 2019 (June 1 – August 31). The project applies Kernel Density Estimation to characterize spatial crime patterns and identify statistically meaningful hotspots across the city's 77 community areas.

## Techniques

| Method | Tool | Purpose |
|---|---|---|
| Univariate KDE | `sklearn.neighbors.KernelDensity` | Crime density vs. distance from city center |
| Bandwidth optimization | Log-likelihood grid search | Kernel + h selection (Epanechnikov, h=0.5 km) |
| Bivariate KDE | `statsmodels.nonparametric.KDEMultivariate` | 2-D hotspot mapping |
| Bandwidth comparison | `normal_reference` vs `cv_ml` | Scott's rule vs cross-validation MLE |
| Geodesic distance | `geopy.distance.geodesic` | Accurate distances on WGS84 ellipsoid |
| Spatial join | `geopandas` + `osmnx` | Commercial land-use correlation |
| Interactive mapping | `folium` | Community area visualization |

## Key Findings

- **Robberies concentrate near the core; homicides shift outward.** Mean distance to city center: 9.00 km (robberies) vs 11.46 km (homicides). Kolmogorov–Smirnov test rejects distributional equality (p < 0.0001).
- **`cv_ml` reveals two distinct homicide clusters** invisible under `normal_reference`. Bandwidth selected by cross-validation is 50–60% narrower than Scott's rule, avoiding the over-smoothing that merges spatially separate risk zones.
- **Robbery rate correlates with commercial zone density (r = 0.63); homicide rate does not (r = −0.28).** The two crime types follow different spatial logics and require different intervention frameworks.

## Project Structure

```
crime-hotspot-detection-kde/
├── chicago_crime_kde_analysis.ipynb
├── data/
│   ├── Chicago_delitos_verano_2019.csv   # Crime records (17,747 rows)
│   └── Areas_comunitarias_Chicago.zip    # Community area shapefiles
├── requirements.txt
└── README.md
```

## Setup

```bash
pip install -r requirements.txt
jupyter notebook chicago_crime_kde_analysis.ipynb
```

---

## Academic Context

This project was developed as part of the **Master's in Analytical Intelligence of Data (MIAD)** program at Universidad de los Andes, Colombia.

---

## Autor

**Joaquín Abondano Araoz** - Data Analytics · AI & Automation · Strategic Planning

[Website](https://joaquinabondano.com) · [LinkedIn](https://linkedin.com/in/joaquin-abondano) · [GitHub](https://github.com/jabondanoaraoz)
