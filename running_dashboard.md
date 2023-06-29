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




## 3. Creating the Dashboard


To visualize and analyze the running data effectively, I utilized Tableau Public. Using a data connector, I exported the cleaned and prepared data from Google Sheets to Tableau Public. This enabled Tableau to dynamically retrieve the updated data from the spreadsheet.
The development of the running data dashboard underwent multiple iterations to provide a comprehensive overview of my overall running progress and mileage. Upon reviewing the data, I observed clear patterns based on my contextual understanding. However, these patterns might not have been immediately apparent to an average viewer. To address this, I decided to enhance the dashboard by incorporating explanatory text to provide better insights into the data.
For example, I discovered a consistent trend of decreased mileage following major goal races, for which I had dedicated several months of training. This drop in mileage was significant and showcased the importance of recovery and post-race downtime.
Additionally, I noticed that my trail race training periods corresponded to an increase in time spent running on trails. By contextualizing this information, viewers can better understand my training focus and the specific preparation for trail races.
Through these additions and explanations, the dashboard now offers a clearer and more informative representation of my running progress and training patterns.


## 4. Key Insights
The created dashboard provided valuable insights regarding my running habits. Firstly, it revealed that I maintained a consistent running schedule during dedicated training blocks. This finding emphasizes the importance of maintaining a certain level of mileage even when not training for a specific event. Going forward, I will be mindful of maintaining this consistency throughout the year.
Secondly, the dashboard showcased a downward trend in my average running pace. This indicates improvements in my overall running performance and suggests that my training efforts have been effective.
Lastly, the analysis highlighted the correlation between the surface I run on and the specific training goals I have. It became evident that my choice of running surface is influenced by the type of race or event I am preparing for. This insight allows me to align my training strategies more effectively based on the specific terrain requirements of my target races.
Overall, these valuable insights gained from the dashboard enable me to enhance my running abilities and deepen my understanding of my training regimen. By leveraging this knowledge, I can become a more informed and efficient runner.

