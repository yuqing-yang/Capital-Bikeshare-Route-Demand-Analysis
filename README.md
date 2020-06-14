# Capital Bikeshare Route Demand Forecasting
Rongkui Han, Miao Hu, Connor Rosenberg, Yuqing Yang

_STA208 Spring Quarter Project_

Please examine "_Capital Bikeshare Final Project.ipynb_" for our full analysis and report.

## Purpose

Capital Bikeshare is a company in Washington, DC which provides local residents, workers, and tourists a method of public transportation. The system operates 591 bike docks across the Washington, DC metro area where users can start and end their commute.

To use the bike network, customers walk to one of these docks and swipe their membership or credit card to unlock one of the station’s bikes. They then bike to another dock near their final destination and return the bike by locking it back into the dock. Unlike other bikeshare services, whose bikes live freely on the street, this dock-to-dock system provides the exact start and end coordinates of every trip. This provides a great base to analyze route dynamics in Washington, DC as we can assume a high degree of integrity from the data.

With 591 stations, the Capital Bikeshare network is used by many residents to commute to their place of work. Since the system provides such a useful service with limited capacity, the morning rush hour can place great strain on the network. For this reason, it is important to develop a method of forecasting a route's demand so workers can strategically place bikes overnight in preparation for riders' daily commute.  

The purpose of this project is to estimate the daily number of trips between each route in the Capital Bikeshare network durring the morning rush. We define the morning rush to take place between the hours of 5:00AM and 10:00AM. We accomplish this task through three primary phases of analysis. First, we cluster each station based on the characteristics of the surrounding destinations. Next, we use these clusters as a new variable to predict if any trips occur along each route. Finally, we then predict how many trips will occur on each route during the morning rush.

## Preparation

### Getting the Data
The data used in this project is quite large, and can not be efficiently uploaded onto Github. Below, we describe the different sources of data used in our analysis in addition to instructions on how to download and process this data for replication.

__Capital Bikeshare Ride Data:__ https://s3.amazonaws.com/capitalbikeshare-data/index.html

The above link directs to a repository of monthly CSV files that contain Capital Bikeshare's ride data from the previous month. For our analysis, we selected all 12 months of ride data from 2019 as our training set and three months of ride data from January, February, and March 2020 as our testing set. The rationale behind this decision was to preserve the time dependence within our data. Instead of a random split into testing and training sets, we chose a split which allowed us to keep a consistent temporal flow to our analysis and use the past to predict the future. 

After downloading the relevant files, unzip each CSV trip dataset and move it to your desired folder. We suggest that you rename each file as “_year-month_” to streamline munging.

In Python, first, import all functions from "_DataPipeline.ipynb_", located in this Github repository. Next, create a list containing the file path of each CSV trip file. Finally, feed this list of file paths into the “ _pipeline()_ ” function. The output will be the major data frame used for phases two and three on this project.

__Geographical Locations of Bike Docks:__ https://opendata.dc.gov/datasets/capital-bike-share-locations/data?page=5

From the above link, download the full CSV dataset for Capital Bikeshare stations and thier geographical locations. Save this file in your working directory and rename it to "_Capital_Bike_Share_Locations.csv_".

## Relevant Notebooks

#### _AssumptionCheck.ipynb_
> Re-runs the analysis from Predicting_Route_Trip.ipynb but on a modified dataset to check certain assumptions we apply to our regression models

#### _Binary_DeepNeuralNet.ipynb_
> Predicting if at least one trip occurs on a given route using deep neural nets.

#### _Binary_RandomForest.ipynb_
> Predicting if at least one trip occurs on a given route using deep random forest models.

#### _Capital Bikeshare Final Project.ipynb_
> Our comprehensive report which includes our relevant analysis and results.

#### _Clustering.ipynb_
> Our station clustering workflow and analysis using the data denerated from "_GetStationTags.ipynb_".

#### _DataPipeline.ipynb_
> Contains the functions required to generate the final datasets used in our analysis. The function "_Pipeline_" uses the cluster assignments, station locations, and raw trip data as input and returns one cohesive data frame which counts the number of trips made each day along each distinct route. 

#### _GetStationTags.ipynb_
> Interfaces with Google Places API to generate the tags of all locations within 250 feet of each station

#### _Predicting_Route_Trip.ipynb_
> Predicting the number of trips which will occur on a given route using: Ridge Regression, Poisson Regression, Random Forest and Gradient Tree Boosting. 


## Relevant Data

#### _Binary_DNN_PR.csv_
> data to generate the percision recall curve for the deep neural net

#### _Capital Bike Share Locations.csv_
> The geo-locations of each Capital Bikeshare station. Obtained from https://opendata.dc.gov/datasets/capital-bike-share-locations/data?page=5

#### _cluster_category_heatmap.csv_
> Data required to generate cluster category heatmap

#### _DNN_ConfMat.csv_
> Confusion matrix for deep neural net's performance on testing data

#### _geo_map.csv_
> Data to generate interactive map of cluster assignments

#### _kernalPCA.csv_
> Data required to generate PCA scatterplots colored by cluster assignment 

#### _Places_near_stations_type_count_matrix_all copy.csv_
> Output from _GetStationTags.ipynb_

#### _RF_ConfMat.csv_
> Confusion matrix for random forest's performance on testing data

#### _station_cluster.csv_
> The station ID and cluster assignment for each station. Generated from _Clustering.ipynb_







