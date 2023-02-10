# Flood Mass Balance Calculations for the Nooksack, 2021

## Project Team
Ingrid Phillips

## Required Packages
pyPRISMclimate

## Required Data
PRISM modeled precipitation and temperature data, for precipitation and snow calculations

USGS river gauge data

SNOTEL data to verify precipitation calculations?

Geology data for infiltration (gSSURGO?), TBD

Evapotranspiration data (this could be LandSat 8 and 9, but obviously those only work on cloud-free days and rain typically means clouds. could provide a regional estimate though?

## Intended Project Structure
1. Notebook 1: Responsible for data retrieval and management. For example: Download PRISM precipitation data, mask data by shapefile or by a DEM raster file
2. Notebook 2: Calculates runoff loss due to snow
3. Notebook 3: Calculates runoff loss due to infiltration
4. Notebook 4: Calculates runoff loss due to evapotranspiration
5. Notebook 5: Calculates runoff modeled - runoff measured, to find discrepancies
