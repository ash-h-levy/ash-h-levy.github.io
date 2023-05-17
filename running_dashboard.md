# Running Data Dashboard 


## 1. Gathering Data


To create a comprehensive running data source, I gathered information from three different apps: Nike Running, Apple Workout, and Garmin Connect. To consolidate the data into a single platform, I utilized an app called Run Gap, which allowed me to upload workouts from Nike and Apple to Garmin. Garmin served as the primary storage for most of my runs and also provided the option to download a CSV file containing detailed workout data.


	
## 2. Data Cleaning and Preparation 


To ensure the accuracy and uniformity of the data, I followed several steps after uploading the CSV file into Google Drive and opening it in Google Sheets. Firstly, I removed irrelevant values from the dataset. By default, Garmin includes data fields that are not pertinent to running and consist of null values.


Next, I standardized the run types by utilizing the IF function. Some runs were labeled simply as "Running" when they should have been categorized as "Road Running." However, the trail, track, and treadmill runs were labeled correctly.




```
=IF(A2="Running", "Road Running", A2)
```
Additionally, I introduced a new column to specify the surface type. By implementing an IFS statement that referenced the activity type, this field populated accordingly.


```
=IFS(A2="Road Running", "Road", A2="Trail Running", "Trail", A2="Track Running", "Track", A2="Treadmill Running", "Treadmill")
```


The final step in the preparation involved converting the average pace field from the original minutes and seconds format to a decimal format, which is necessary for subsequent calculations. Both spreadsheets and Tableau do not recognize the original format. To achieve this, I used the LEFT and RIGHT functions to split the time values into minutes and seconds. Subsequently, I converted the seconds to a decimal by dividing them by 60. Finally, I added the minutes and the seconds as a decimal to obtain the desired format.
