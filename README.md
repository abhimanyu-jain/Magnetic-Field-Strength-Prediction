# Magnetic-Field-Strength-Prediction

Introduction

This project aims to predict magnetic field strength based on historical data. 3 satellites measured magnetic field strength at various points around the earth over several years.

The points around the earth are represented with the following Geomagnetic coordinates:

1. L value https://en.wikipedia.org/wiki/L-shell
2. Magnetic Local Time (MLT) 
3. Magnetic Latitude (MLAT)

Time is represented using Year, Month, Day, Hour, Minute and Second.


 AL index and KP index are commonly used magnetic activity indices.
	https://www.ngdc.noaa.gov/stp/solar/magindices.html


Satellite flag represents which satellite took the reading.

Bw is the output, also called the Magnetic Flux Density https://en.wikipedia.org/wiki/Magnetic_flux.


Exploratory Data Analysis

Data was collected from 2010 to 2018.

There were 255752 rows with null/NaN value in column 'B', other columns did not have any null/NaN values. These rows were dropped.



Data engineering


'MLT' values had to be converted to float values.

'Year', 'Month', 'Day', 'Hour', and 'Minute' were combined into a 'Datetime' column.

Columns 'year', 'month', 'day', 'hour', 'minute', 'AL Index', 'KP Index', 'Satellite Flag' were dropped.

Sorting 'B' values and plotting them shows that they exist on an exponential distribution.

Now we will split the area defined by L, MLT and MLAT into different regions and run LSTM for each region

For L, the values range from 2-10
For the Earth, L-shells uniquely define regions of particular geophysical interest. 
Certain physical phenomena occur in the ionosphere and magnetosphere at characteristic L-shells. 
For instance, auroral light displays are most common around L=6, 
can reach L=4 during moderate disturbances, and during the most severe geomagnetic storms, may approach L=2. 
The Van Allen radiation belts roughly correspond to L=1.5-2.5, and L=4-6. The plasmapause is typically around L=5.

Four Magnetic Local Time (MLT) sectors are considered, leading to four different K-derived MLT sector indices: 
   aσDawn     (03–09 MLT), 
   aσNoon     (09–15 MLT), 
   aσDusk     (15–21 MLT), 
   aσMidnight (21–03 MLT) indices. 
 They cover more than four solar cycles and, thus, allow robust statistical analysis.
 Link : https://www.researchgate.net/publication/260329903_The_K-derived_MLT_sector_geomagnetic_indices


'MLAT' is split in sections each with a differential range of 5.

Once we have the dataframe split into sectors, we get 140 dataframes.

We can now drop 'L', 'MLT' and 'MLAT' columns.



Models

# LSTM
# ARIMA
# ARCH
# VAR