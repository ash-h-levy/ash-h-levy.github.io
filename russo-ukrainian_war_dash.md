
# Russian Losses in Russo-Ukrainian War Dashboard Using Tableau Public and Google Sheets

## 1. Getting the Data 

The data was sourced from [Kaggle](https://www.kaggle.com/datasets/piterfm/2022-ukraine-russian-war?select=russia_losses_equipment.csv). This dataset was created by a Ukrainian developer using data from official sources. 

## 2. Data Cleaning in Google Sheets

To clean the data, it was uploaded to [Google Sheets](https://docs.google.com/spreadsheets/d/1uIm3k2pBrlUzFm_mRHaSYpQWVqVXjivtTLzFpkv6PNQ/edit?usp=sharing).



Certain fields had been combined over time. For instance, "Military Auto" and "Fuel tanks" were merged into "Vehicles and Fuel Tanks," while "Mobile SRBM System" was consolidated into "Cruise Missiles." However, during the combining process, the old data was not transferred to the new category, and any data recorded after the merge was not included in the original category. To ensure data continuity and prevent loss during further analysis, I moved all the values to their respective combined categories. Fortunately, the personnel data did not require any cleaning.

Subsequently, I created a new sheet to calculate the daily losses by implementing formulas such as:


```
=equipment_cummlative!C3-equipment_cummlative!C2
```

This process was also applied to the personnel data for calculating daily losses.


## 3. [Creating the Dashboard](https://public.tableau.com/app/profile/ashley.levy8624/viz/RussianLossesinRusso-UkrainianWar/Dashboard23) 

I connected the data sheet to Tableau Public and encountered an issue with the format. The data was in a wide format, which made it difficult to create a stacked area chart for equipment losses. To overcome this, I used Tableau's pivot functionality to transform the data into a suitable format for the desired chart.

Initially, I had both the equipment and personnel data on a single dashboard. However, after careful consideration, I decided to separate them into two distinct dashboards for better clarity and focus.

To provide a quick overview of the losses, I included scorecards that display the total losses and highlight the overall impact. These scorecards enable users to get a clear picture of the magnitude of the losses.

Additionally, I incorporated a stacked area chart and bar charts to showcase the rate at which the losses occurred. These visualizations offer valuable insights into the intensity of the fighting and facilitate a deeper understanding of the data.
