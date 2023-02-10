# Flood Mass Balance Calculations for the Nooksack, 2021

## Project Team
Ingrid Phillips

## Project Summary
This project aims to create a JupyterNotebook workflow for performing a precipitation-runoff mass balance on a watershed, using the 2021 Nooksack River floods as a case study. 

## Background Information

## Objectives
Use a mass-balance study to determine the accuracy of USGS gauges during extreme precipitation events, using the 2021 atmospheric river flooding on the Nooksack as an example. The final product will probably look like a time series, daily modeled runoff vs. daily measured runoff.

This project can have levels of complexity. The bare minimum in general is calculating the volume of precipitation - volume of discharge. My minimum goal is to at least incorporate snow deposition. Infiltration would make this workflow more universally reproducible, but the soils are typically assumed to be saturated before the atmospheric river in the Nooksack so it isn't super relevant for this use-case. Evapotranspiration is something that I need to do more research into, to see if it would even make an impact with cloud cover. Infiltration and evapotranspiration are both "hopefuls" more than minimums. The 'extra mile' goal is to run the scripts a few times for a sensitivity analysis to see how snow, infiltration and evaporation make significant impacts. A more complex model is not necessarily a better model if the added parameters don't make a big impact and they add a lot of uncertainty (really coarse geology data could be relevant here).


## Required Data
PRISM modeled precipitation and temperature data, for precipitation and snow calculations

USGS river gauge data

SNOTEL data to verify precipitation calculations?

Geology data for infiltration (gSSURGO?), maybe land use (there are some papers on this), TBD

Evapotranspiration data (this could be LandSat 8 and 9, but obviously those only work on cloud-free days and rain typically means clouds. could provide a regional estimate though?

## Required Packages
pyPRISMclimate allows for the streamlining of downloading weather data - https://sdtaylor.github.io/pyPRISMClimate/




## Intended Project Structure
1. Notebook 1: Responsible for data retrieval and management. For example: Download PRISM precipitation data, mask data by shapefile or by a DEM raster file
2. Notebook 2: Calculates runoff loss due to snow
3. Notebook 3: Calculates runoff loss due to infiltration
4. Notebook 4: Calculates runoff loss due to evapotranspiration
5. Notebook 5: Calculates runoff modeled - runoff measured, to find discrepancies
