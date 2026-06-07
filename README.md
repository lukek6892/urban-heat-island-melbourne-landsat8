# Urban Heat Island Analysis — Melbourne
### Land Surface Temperature Mapping using Landsat 8 Thermal Remote Sensing

**Author:** Luke Kennedy
**Date:** June 2026
**Tools:** ArcGIS Pro, USGS EarthExplorer
**Data:** Landsat 8 Collection 2 Level-1 (USGS), ABS Greater Melbourne Boundary

---

## Overview
This project derives and analyses Land Surface Temperature (LST) across Greater Melbourne 
using Landsat 8 Band 10 thermal infrared imagery. The analysis follows a six-step 
processing chain to quantify surface temperature variation across the metropolitan area, 
identifying urban heat island patterns and the moderating role of vegetation and water bodies.

The scene used is from **February 2020**, representing Melbourne's late summer thermal 
peak. The study area is clipped to the Greater Capital City Statistical Area (GCCSA) 
boundary for Greater Melbourne.

---

## Methodology
The following six-step processing chain was applied in ArcGIS Pro Spatial Analyst 
Raster Calculator:

| Step | Output | Formula |
|------|--------|---------|
| 1 | TOA Radiance | `L = 0.0003342 × B10 + 0.1` |
| 2 | Brightness Temperature | `BT = 1321.0789 / Ln(774.8853 / L + 1) − 273.15` |
| 3 | NDVI | `(B5 − B4) / (B5 + B4)` |
| 4 | Proportion of Vegetation | `Pv = Square((NDVI − NDVImin) / (NDVImax − NDVImin))` |
| 5 | Land Surface Emissivity | `LSE = 0.004 × Pv + 0.986` |
| 6 | Land Surface Temperature | `LST = BT / (1 + (0.00115 × BT / 1.4388) × Ln(LSE))` |

Thermal constants used: K1 = 774.8853, K2 = 1321.0789 (Landsat 8 Band 10).
All processing conducted at 30m spatial resolution.

---

## Data Sources
- **Landsat 8 OLI/TIRS Collection 2 Level-1** — USGS EarthExplorer (earthexplorer.usgs.gov)
  - Scene: LC08_L1TP_092086_20200223
  - Bands used: Band 4 (Red), Band 5 (NIR), Band 10 (TIR)
- **Greater Melbourne Boundary (GCCSA)** — Australian Bureau of Statistics (abs.gov.au)

---

## Key Findings
- LST across Greater Melbourne ranged from approximately **13.24°C to 37.80°C** in February 2020
- The urban core and western suburbs exhibited the highest surface temperatures, 
  consistent with high impervious surface density and limited canopy cover
- The Yarra Valley, Dandenong Ranges fringe, and Port Phillip Bay coastline acted 
  as primary thermal buffers, registering the lowest LST values in the scene
- NDVI is a strong inverse predictor of LST — suburbs with higher vegetation 
  fraction showed measurably lower surface temperatures

---

## Map Outputs
*See /outputs folder for full resolution maps*

### Land Surface Temperature — Melbourne, February 2020
![LST Map](outputs/MEL_Land_Surface_Temperature_Feb2020.png)

### NDVI — Melbourne, February 2020
![NDVI Map](outputs/MEL_NDVI_Feb2020.png)


---

## Policy Context
Melbourne faces a well-documented urban heat challenge. The **City of Melbourne Urban 
Forest Strategy** and **Victorian Urban Cooling Strategy** both identify surface 
temperature reduction as a priority. This analysis provides evidence of the spatial 
distribution of heat across the metropolitan area, supporting the case for targeted 
greening interventions in Melbourne's western and northern growth corridors.

---

## Repository Structure
```
/outputs        ← exported map images (PNG, 300 DPI)
/docs           ← PDF report
README.md
```
