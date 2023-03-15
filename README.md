# Aolian_Veg_Models_OilGas
This repository contains data derived from MODIS albedo data (MCD43A3) and spatial data of study sites on the Northern Colorado Plateau. These data were used in the Aeolian Vegetation Models project.

# Authors
Gayle Tyree (1), Nicholas Webb (2), Adrian Chappell (3), Saroj Dhital (2)

# Created 
2021 - 2022

# Purpose
The CW16 data were created to measure the effect of oil and natural gas disturbance on surface roughness (quantified as surface wind friction velocity scaled by 10-m wind speed. These data were retrieved for sites located on five climate-soil-geomorphic groups in the Uinta-Piceance Basin on the northern Colorado Plateau.

# Data
Surface roughness was modeled from black-sky albedo (BSA) produced by the Moderate Resolution Imaging Spectroradiometer (MODIS) MCD43A3 Version 6 product (500-m daily resolution; Schaaf and Wang 2015) using the model developed by Chappell and Webb (2016) (hereafter CW16 model). Pixels contaminated by snow cover were masked prior to modeling using the MODIS MOD10A1 Version 6 Terra Snow Cover Dataset (Hall et al. 2016). 

To characterize surface roughness, the CW16 model takes the inverse of BSA to obtain surface shadow (ω). The shadow is normalized by the isometric parameter of the MODIS Bidirectional Reflectance Distribution Function (f_iso), to remove the spectral reflectance component of surface characteristics unrelated to surface structure that influence albedo, such as soil moisture and color. The model then rescales ω_n between 0.0001 and 0.1 to match the calibration data from Marshall (1971) to get the normalized scaled shadow (ω_ns). This metric has a strong inverse relationship with the surface wind friction velocity u_(S*) scaled by the freestream wind speed U_h, which is calculated as:

Eq. 1			u_(S*)/U_h   = 0.0306(〖2.7183〗^(〖〖-ω〗_ns〗^1.1202/0.0125)  )+0.0072.

The metric u_(S*)/U_h  can then be multiplied by a wind speed (m s-1) to obtain the wind friction velocity acting on the exposed soil surface (u_(S*)), which can then be used to calculate the horizontal sediment flux (Q) for a given threshold friction velocity (u_(*t)) and dust emission (F). Monthly mean u_(S*)/U_h  for each year of the study period was used to calculate probability distributions of u_(S*)/U_h  for disturbed and undisturbed sites (i.e., pixels) within each SGU strata. We ran the model in Google Earth Engine using data from MODIS Band 1 (red; 620-670nm). 

Site selection: We identified disturbed and undisturbed sites from five climate-soil-geomorphic groups (Nauman et al. 2022) located in the Uinta-Piceance Basin of northeast UT/northwest CO to compare the effect of oil/gas activity on modelled surface roughness. Spatial data of oil/gas well pads and access roads were sourced from Villarreal et al. (2023). Pixels were considered disturbed if they contained at least 3,500 m2 of active well pad, which is the median area of mapped active well pads in the UP. A minimum distance of 1000 m was set between the sampled pixels. A minimum of eighteen disturbed pixels was required from each stratum for statistical analysis; if fewer pixels were available, then the stratum was not used in the study. We selected undisturbed pixels based on the following criteria: they had to be from the same SGU-climate stratum, 1000 – 4000 m from the disturbed pixel, contain no oil/gas disturbance (including plugged and abandoned pads and access roads), and could not be directly adjacent to another identified reference pixel. We visually inspected pixels that met these criteria in Google Earth Pro (Google Earth 7.3, 2022) to ensure that none included unmapped development and that they were reasonably comparable to undeveloped areas of disturbed pixels in the same stratum. 

# Data files included:
1. USUh_data_v2.csv
2. Study_sites.zip

# Column descriptions
UID (both files): Unique identifier of the spatial point for which the data were retrieved.

Stratum (both files): The climate-soil-geomorphic group that a given site falls within. The climate-soil-geomorphic groups are sourced from USGS maps of Ecological Site Groups and Soil-Geomorphic Units for the Upper Colorado River Basin (Nauman et al. 2022). ALU = Arid-warm Loamy Uplands, ASH = Arid-warm Saline Hills, SFU = Semiarid-warm Finer Uplands, SLU = Semiarid-warm Loamy Uplands, SVS = Semiarid-warm Very Shallow. 

featTyp (both files): Presence or absence of oil and gas disturbance in the MODIS pixel that the site falls within. As a 16-year time series of us*/Uh is retrieved for each pixel, 'featTyp' of many pixels changes over time from "undisturbed" to "disturbed"; this change corresponds to the value in 'spuddate'. 

spuddate (both files): The date of "spudding" or initial drilling of the well bore, which approximates the initial date of oil and gas disturbance for the pixel. Spud dates of '1/1/1999' indicate that wells in that pixel lacked a spud date record, but the date of initial disturbance was determined to have occurred prior to the year 2000 using the LandTrendr tool (Kennedy et al. 2010).

Date (CSV only): The year and month of us*/Uh retrieval. 

USUh (CSV only): us*/Uh data retrieved from MODIS albedo using the CW16 model. Values are monthly means. 

n (CSV only): The size of the sample (Stratum x featTyp) for the given date. 

# Notes
NSF Grant # 1853853
Title: Collaborative Research: NSFGEO-NERC: Aeolian dust responses to regional ecosystem change

# References
Chappell, A. & Webb, N.P. (2016). Using albedo to reform wind erosion modelling, mapping and monitoring. Aeolian Research, 23, 63-78. https://doi.org/10.1016/j.aeolia.2016.09.006.

Hall, D.K., Salomonson, V.V. & Riggs, G.A. (2016). MODIS/Terra Snow Cover Daily L3 Global 500m Grid. (Version 6) [Data set]. https://nsidc.org/data/mod10a1/versions/6. 

Kennedy, R.E., Yang, Z. & Cohen, W.B. (2010). Detecting trends in forest disturbance and recovery using yearly Landsat time series: 1. LandTrendr—Temporal segmentation algorithms. Remote Sensing of Environment, 114(12), 2897-2910. https://doi.org/10.1016/j.rse.2010.07.008.

Marshall, J.K. (1971). Drag measurements in roughness arrays of varying density and distribution. Agricultural Meteorology, 8, 269-292. https://doi.org/10.1016/0002-1571(71)90116-6.

Nauman, T.W., & Duniway, M.C. (2021). Soil geomorphic unit and ecological site group maps for the rangelands of the Upper Colorado River Basin region: U.S. Geological Survey data release, https://doi.org/10.5066/P92OPRMV.

Schaaf, C. & Wang, Z. (2015). MCD43A3 MODIS/Terra+Aqua BRDF/Albedo Daily L3 Global - 500m. (Version 006) [Data set]. https://doi.org/10.5067/MODIS/MCD43A3.006.

Villarreal, M.L., Chambers, S.N., Duane, O.M., Duniway, M.C., Tyree, G., Waller, E.K. (2023). Maps of oil and gas pads and access roads on the Colorado Plateau, Utah, Colorado, and New Mexico: U.S. Geological Survey data release. [doi pending]
