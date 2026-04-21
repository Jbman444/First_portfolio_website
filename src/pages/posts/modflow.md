---
layout: ../../layouts/MarkdownPostLayout.astro
title: Groundwater Flow Modeling with MODFLOW 6
description: "A steady-state groundwater model developed using FloPy, incorporating well observations, topography, and conceptual hydrogeologic boundaries."

image:
  url: "/images/modflow_colton/colton_1.png"
  alt: "Final hydraulic head contour map"

imageDark:
  url: "/images/modflow_colton/colton_1.png"
  alt: "Final hydraulic head contour map"
tags: []
---



# Groundwater Flow Modeling Report

## 1. Objective

The objective of this study was to develop a **steady-state groundwater flow model** using MODFLOW 6 to:

* Represent regional groundwater flow patterns
* Incorporate observed well data
* Evaluate model performance through residual analysis

---

## 2. Topographic Surface

<img src="/images/modflow_colton/colton_2.png" alt="Interpolated topographic surface used as model top elevation" />

The model top elevation was derived from raster topography and interpolated onto the model grid.
This surface defines the **upper boundary of the aquifer system** and controls hydraulic gradients.

---

## 3. Initial Head Representation (Interpolation-Based)

<img src="/images/modflow_colton/colton_3.png" alt="Initial interpolated head field showing unrealistic artifacts" />

An initial attempt used interpolation of well heads to define the hydraulic field.

### Observations

* Visible interpolation artifacts
* Non-physical triangular gradients
* Poor representation of regional flow

### Conclusion

This approach was **not suitable**, as it lacked physical grounding.

---

## 4. Recharge Distribution

<img src="/images/modflow_colton/colton_4.png" alt="Recharge array showing elevated recharge near river buffer zones" />

Recharge was applied as:

* Uniform background recharge across the domain
* Increased recharge in **river buffer regions**

This represents **ephemeral stream recharge during wet seasons**.

---

## 5. Conceptual Model Development

A conceptual hydraulic gradient was implemented:

* **Northwest**: High head (upland recharge zone)
* **Southeast**: Low head (valley discharge zone)
* Flow expected:

  * NW → SE
  * NE → SE

Boundary conditions were defined using **constant head (CHD) boundaries** consistent with this conceptual model.

---

## 6. Simulated Steady-State Head

<img src="/images/modflow_colton/colton_5.png" alt="Simulated steady-state hydraulic head distribution" />

The resulting head field shows:

* Smooth gradients across the domain
* Physically realistic flow patterns
* Alignment with expected regional groundwater movement

---

## 7. Hydraulic Head Contour Map

<img src="/images/modflow_colton/colton_6.png" alt="Hydraulic head contour map showing groundwater flow direction" />

Hydraulic head contours illustrate the regional flow system.

### Interpretation

* Groundwater flows **perpendicular to contour lines**
* Flow direction generally follows:

  * Northwest → Southeast
  * Northeast → Southeast

Contour spacing indicates variations in hydraulic gradient.

---

## 8. Observed vs Simulated Heads

<img src="/images/modflow_colton/colton_7.png" alt="Simulated head field with wells colored by observed head values" />

Well locations are colored by **observed hydraulic head values** and plotted over the simulated field.

### Interpretation

* Provides direct visual comparison between model and field data
* Highlights areas where simulated heads deviate from observations

---

## 9. Residual Analysis

<img src="/images/modflow_colton/colton_8.png" alt="Residual map showing difference between observed and simulated heads" />

Residuals were computed as:

Observed Head − Simulated Head

### Interpretation

* **Positive residuals** → model underestimates head
* **Negative residuals** → model overestimates head

### Observations

* Most wells fall within ±5–20 m
* Larger discrepancies observed at:

  * Site 1 (underprediction)
  * Site 4 (overprediction)

---

## 10. River System Overlay

<img src="/images/modflow_colton/colton_7.png" alt="River system overlay on groundwater model domain" />

The river network was incorporated using buffered recharge zones.

### Notes

* Rivers are **ephemeral**, flowing primarily during winter
* Modeled as recharge sources only
* Do not currently represent discharge conditions

---

## 11. Model Performance Summary

| Site   | Observed (m) | Simulated (m) | Residual (m) |
| ------ | ------------ | ------------- | ------------ |
| Site 1 | ~332         | ~315          | -16 to -18   |
| Site 2 | ~291         | ~307          | +15 to +18   |
| Site 3 | ~275         | ~282          | +6 to +9     |
| Site 4 | ~264         | ~289          | +24 to +28   |
| Site 5 | ~278         | ~283          | +5 to +9     |

---

## 12. Discussion

### Strengths

* Captures regional groundwater gradient
* Produces stable and interpretable results
* Aligns with conceptual hydrogeologic understanding

### Limitations

* Simplified steady-state conditions
* River system treated only as recharge
* Local-scale processes not explicitly modeled

---

## 13. Conclusions

This model represents a **defensible first-order groundwater simulation**:

* Successfully reproduces regional flow behavior
* Integrates observed data and conceptual understanding
* Provides a foundation for further refinement

Residual patterns suggest that:

* Site 1 may be influenced by localized recharge
* Site 4 may require representation of discharge processes

---

## 14. Future Work

* Implement **RIV or DRN package** for stream interaction
* Develop a **transient model** to capture seasonal dynamics
* Incorporate spatially variable recharge datasets
* Use **MODPATH** for particle tracking and transport analysis

---

## 15. Tools & Skills

* Python (NumPy, SciPy, Pandas)
* FloPy / MODFLOW 6
* Rasterio
* QGIS
* Hydrogeologic modeling

---

## Notes

This project demonstrates a complete workflow from raw data processing to numerical groundwater simulation, emphasizing conceptual model development and iterative refinement.


## Experimental Work: Developing 3D Lithology Maps

An ongoing area of development in this project is the construction of experimental 3D lithology maps to better represent subsurface heterogeneity in groundwater models. The goal is to use borehole data together with spatial prediction methods, such as kriging and related interpolation or classification approaches, to estimate hydrofacies between known data points.

By moving from sparse borehole observations to a more continuous 3D representation of subsurface materials, this workflow aims to improve the characterization of aquifer structure and flow pathways. A better hydrofacies model can support more realistic groundwater flow simulations and, in future work, help improve analyses related to land subsidence and aquifer-system response.

This work is still under development, but it represents an important next step toward integrating geologic uncertainty, spatial prediction, and groundwater modeling into a more complete hydrogeologic framework.

## 3D Hydrofacies Visualization

<div class="visual-3d-frame">
  <iframe
    src="/predictedGeology.html"
    title="3D hydrofacies visualization"
    loading="lazy"
  ></iframe>
</div>

<p class="figure-caption">
  Experimental 3D lithology model produced from machine learning hydrofacies predictions based on borehole data. This developing workflow is intended to improve subsurface characterization for future groundwater flow and subsidence analysis.
</p>





