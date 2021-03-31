# melbourne-parking

## Introduction
 “The City wants to look at removing some on-street public parking to make the area nicer and more amenable to public transport and pedestrians, and at optimising their park bay restrictions to minimise breaches. They are asking for recommendations from you on whether and how they should do this.”
 The problem is twofold, look for a way to identify parking bays that could be removed, and look to optimise parking limits while remaining fair.
 The approach I took in the end, was to determine how a bay was being used compared to signed limits, and what proportion of time it spent empty.
 Exploration - Pandas and Excel
 The datasets used in the end were the “On-street Car Parking Sensor Data 2017”, “On-street Parking Bays (Spatial Polygons)” and the “On-street_Parking_Bay_Sensors” from City of Melbourne Open Data.
 Initial exploration of the data was performed to understand what each record means for each dataset, and what strategy could be used to approach the client’s problem statements. For the main 2017 dataset, each row was a “parking event”. Each event was timestamped when it started, which could occur when a bay goes from vacant to filled, a bay goes from filled to vacant, the date changes, or the parking sign in effect changes.
  
## Cleaning - Pandas
 Performed in the Jupyter Notebook “Cleaning”. The input was initially the raw data provided by Melbourne City.  The 2017 data initially required a format change for the DateTime columns, this was run only once as it took considerable time to process. From then on the data was cleaned from a file saved after this process.
 The process required was commented on throughout, but some of the major obstacles were faulty sensor readings, and the requirement to work on the “sign” column to extract information. This was because the “On-street Car Park Bay Restrictions” dataset did not merge well with the 2017 data, too many signs had been changed since 2017.
 Analysis
 Pandas
 The Jupyter Notebook “Analysis” contains different sections where different slices of the original 2017 dataset are used. Different parameters were used to get an overall understanding of the 2017 data and glean the surface of insights into motorist behavior using matplotlib and seaborn.
 The original idea was to make it more modular and manageable if I were to merge other datasets onto slices. This was the idea for the “Merge, Divide and Conquer” notebook. In the end, the merge notebook was only used to add spatial data to an aggregated bay dataset.
 Tableau Dashboard
 The goal of the Tableau dashboard is to create an interactive way to view the utilisation of parking, using filtering and parameters. Spatial data is included to provide a map view.
  
## Data Handling
 Downloaded from:
 https://data.melbourne.vic.gov.au/browse?sortBy=most_accessed&src=fp_tile
 1.	On-street Car Parking Sensor Data 2017
 2.	On-street Parking Bays (Spatial Polygons)
 3.	On-street Parking Bay Sensors
 https://www.ptv.vic.gov.au/footer/data-and-reporting/datasets/
 1.	Tramlines spatial data
### Cleaning.ipynb:
 Input
 1.	On-street_Car_Parking_Sensor_Data_-_2017.csv (Initial, but started in future from partially cleaned file due to DateTime conversion time required)
 2.	On-street_Car_Parking_Sensor_Data_-_2017_cleaned.csv
 3.	On-street_Parking_Bays.csv
 4.	On-street_Parking_Bay_Sensors.csv
 Output
 1.	parking_2017_cleaned.csv
 2.	parking_2017_cleaned_vehicle_present.csv
 3.	parking_2017_cleaned_violation.csv
 4.	bay_geom_cleaned.csv
 5.	Parking_sensors_cleaned.csv
  
### Analysis.ipynp
 Input
 1.	parking_2017_cleaned.csv
 2.	parking_2017_cleaned_vehicle_present.csv
 3.	parking_2017_cleaned_violation.csv
 Output
 1.	bays_2017.csv
 Merge, Divide and Conquer.ipynb
 Input
 1.	bay_geom_cleaned.csv
 2.	parking_sensors_cleaned.csv
 3.	Bays_2017.csv
 Output
 1.	tableau_bays.csv
## Data Problems
 Lack of live sensor data (~2500 sensors at the time of last pull, when supposed to be 4600), which was the only co-ordinate system available. Led to blank spots in the Tableau mapping stage. Overlaid map with a .shp file of parking bays, but there was an oversupply of bays compared to the sensors (6000 bays compared to 4600 sensed bays). Would recommend improving the availability of functional sensors for analysis.
 The way events were created both helped and hindered the analysis. It allowed a look into violations and durations while a sign was active, but also meant overall parking duration was very hard to obtain. In the end, I used the positives and set the merging of events as an action for “next steps”.
