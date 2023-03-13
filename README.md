# Flood Mass Balance Calculations for the Nooksack, 2021

## Project Team
Ingrid Phillips

## Project Summary
This project aims to create a JupyterNotebook workflow for performing a precipitation-runoff mass balance on a watershed, using the 2021 Nooksack River floods as a case study. 

## Background Information

The goal of this project is to get a window into the accuracy of flood gauges during extreme precipitation events, with the hypothesis being that sediment deposition or scour could change the channel cross-sectional area, which would introduce error to the gauges. However, the accuracy of other datasets such as modeled precipitation data or snowfall could also be explored with this analysis. 

## Objectives
Use a mass-balance study to determine the accuracy of USGS gauges during extreme precipitation events, using the 2021 atmospheric river flooding on the Nooksack as an example. The final product is a graph showing the % difference between modeled runoff and measured discharge over time.

At the present, this project involves downloading PRISM modeled climate data constrained by a USGS gage basin, calculating snow fall from precipitation and temperature, and then using precipitation and snow accumulation to calculate the projected runoff in the system. This is then compared to the USGS gage discharge volume from the same period. The main notebooks rely on PRISM, but there is a data_alternative notebook which explores Daymet instead.

General model data verification information needs to be added to the workflow, including using CO-OP and SNOTEL stations to verify precipitation and snow.

This project is still in development. Adding infiltration runoff removal would make this workflow more universally reproducible, but the soils are typically assumed to be saturated before the atmospheric river in the Nooksack so it isn't relevant for this use-case at this time. Evapotranspiration is something that I need to do more research into, to see if it would even make an impact with cloud cover. It may not make an impact during a winter-season storm in the PNW, but could matter more for other ecosystem. A more complex model is not necessarily a better model if the added parameters don't make a big impact and they add a lot of uncertainty (really coarse geology data could be relevant here).


## Required Data
Currently in use:
* PRISM modeled precipitation and temperature data, for precipitation and snow calculations
  * https://prism.oregonstate.edu/recent/monthly.php

* USGS river gauge data
  * https://waterdata.usgs.gov/nwis/rt

* Daymet climate data
  * https://daymet.ornl.gov/

Not in use, but may be incorporated in the future:
* COOP and SNOTEL data to verify precipitation and snow depth modeled values
  * https://www.ncei.noaa.gov/products/land-based-station/cooperative-observer-network
  * https://wrcc.dri.edu/snotel/

* Geology data for infiltration (gSSURGO?), maybe land use (there are some papers on this), TBD
  * https://mrdata.usgs.gov/geology/state/map-us.html
  * https://www.usgs.gov/centers/eros/science/national-land-cover-database

* Evapotranspiration data (this could be LandSat 8 and 9, but obviously those only work on cloud-free days and rain typically means clouds. could provide a regional estimate though?
  * https://earlywarning.usgs.gov/ssebop/modis/daily/626

## Required Packages
* pyPRISMclimate for downloading climate data - https://sdtaylor.github.io/pyPRISMClimate/
* pyDaymet for downloading climate data
* hydrofunctions for downloading streamflow and basin metadata
* rasterio for raster data set analysis  
* xarray for data set analysis
* numpy, pandas, and matplotlib for general calculations and plotting
* geopandas for geodataframes and retrieving shapefiles
* glob, os, and sys for managing files

## Intended Project Structure
1. data_download.ipynb: Responsible for data retrieval and management. For example: Download PRISM precipitation data, mask data by shapefile or by a DEM raster file
2. snow_volume_calculations.ipynb: Calculates runoff loss due to snow
3. Does not exist yet: Notebook 3: Calculates runoff loss due to infiltration
4. Does not exist yet: Notebook 4: Calculates runoff loss due to evapotranspiration
5. mass_balance.ipynb: Calculates runoff modeled - runoff measured, to find discrepancies
note there is currently also the data_alternative.ipynb which explores Daymet climate data as an alternative to PRISM

# Current Project Status - 3/10/2023

**Data download, snow volume calculations, and mass balance files are operational!**

There is a **lot of discrepancy** in the final calculated runoff compared to the measured river discharge. Some potential ways to address that, and find where the error is coming from:
 * Use CO-OP stations to verify/unverify the accuracy of PRISM dataset
 * Use SNOTEL data to test the snow accumulation/melt
 * Try some different gridded precipitation datasets, like Daymet (1 km resolution) and Livneh (6 km resolution)
 * Test on another watershed or during another, smaller storm that occurs during the summer when we wouldn't anticipate significant snow accumulation
 
 Beyond the data verification process suggested above, next steps include:
 * Calculating and subtracting baseflow
 * Accounting for infiltration and evapotranspiration
 * Testing on other watersheds (how broadly does this process apply?)
