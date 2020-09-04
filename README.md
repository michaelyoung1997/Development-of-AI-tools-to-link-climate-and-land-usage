# Development-of-AI-tools-to-link-climate-and-land-usage

This repository contains 5 Python notebooks as supplementary material for the submission of my master's dissertation as part of the MiSCADA course. 

Each notebook requires the assignment of a path variable which contains a string of the filepath to the Data folder. 


**(Air Temperature) Data Preparation**
Generates dataframes from Met Office weather station monthly readings, altitude data sourced from Google Earth Engine and UKCEH land cover map

**Air Temperature Data Analysis** 
Uses aforementioned dataframe to predict air temperature readings using various regression algorithms then seeks to classify the polarity of the residual using land cover information. Also attempts to use a GAN to generate synthetic training data to improve model performance. 
This code has not been formatted neatly as it was used purely to generate results for the final report. 

**Surface Temperature Data Preparation**
Generates dataframes for randomly stratified sampled points using MODIS LST readings and other land attributed sourced from Google Earth Engine, soil information from combined England and Scotland soil map and UKCEH land cover map.  

**Surface Temperature Data Analysis**
Uses aforementioned dataframe to predict air temperature readings using various regression algorithms then seeks to classify the polarity of the residual using land cover information. The code has been formatted into a model class, usage explained below.


*Initialize model* 

-model=my_model(dataframe, axis=1), target)

-dataframe=lst15 or lst07 
-target='Feb_2015_LST', 'Jul_2015_LST', 'Nov_2007_LST' (or any other column from the targets dataframe) 

*Perform Regression* 

-model.regression(method, poly, features)

-method='boost', 'bag' or 'lasso' 
-poly= 1 or 2 
-features=features to perform regression with

*Generate Residuals*

-model.residuals(binary=True)

*Classify Residuals*

-model.classify_residuals(classifier='xgboost', poly=2) 

-classifier='nn', 'xgboost', 'rf'

*Generate table of feature importances and correlations*

-frame=model.importances() 

**Kriging Spatial Analysis** 
Generates semivariograms for altitude and LST. 
Uses a 25gb runtime, as opposed to the regular 12gb which runs out of memory
