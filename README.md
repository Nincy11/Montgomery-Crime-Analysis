# Montgomery-Crime-Analysis

<img width="664" alt="Screenshot 2023-12-25 at 6 41 58 pm" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/41fa8a12-1347-4d4a-8840-725f43eea06e">


Overview of the dataset
The dataset presents the crime details occurred in the Montgomery County in the state of Maryland in USA. It includes all founded crimes reported after July 1st, 2016, and are entered to-date utilizing Uniform Crime Reporting (UCR) rules. The dataset has the title ‘Crime’ and is acquired from Montgomery County’s open data website. It is open to public access and utilisation. The data is derived from the reported crimes classified according to the National Incident-Based Reporting System (NIBRS) of the Criminal Justice Information Services (CJIS) Division Uniform Crime Reporting (UCR) Program and documented by approved police incident reports. The dataset used for this experiment is real-time and is updated daily. The dataset is in a csv file with a structured format. The dataset is about 80 MB in size and consists of 317339 rows and 30 columns. A total of 291255 crimes with unique Incident ID have been reported in the dataset. It contains not only reported crimes but also attempted ones which are not further classified. Multiple offenses were reported for 26,084 crimes and each of these offenses may have multiple victims. The dataset also comprises of crimes that are not yet verified by further investigation.

##Crime Dataset Pre-processing 

1. Dealing Missing values:
<img width="452" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/3da25c65-ff0f-49fd-b431-85d82c525ff7">

Dropping the column: Street Prefix’ and ‘Street Suffix’ columns can be dropped since more than 95% of the entries are null and there is already pertinent information available describing the crime's location. 
Imputing values with Mean: About 50% of data in End Date Time’ is empty but these entries cannot be dropped as its crucial to calculate the duration of crime. Since the End Date Time cannot potentially exceed the time of the Police arrival, the empty entries in this column can be supplied with the matching Dispatch Date/Time values, if available. The remaining missing values in this field can be filled with the sum of average response time and Start Date Time. 

3. Removing Irrelevant data: The dataset can be made more intelligible and compact by filtering out the attributes that do not contribute anything useful to the understanding of the data. Hence, the below attributes are removed:
Incident ID, CR Number, Location, Police District Number, Block Address, Address Number, Zip Code, Sector/Beat/PRA.

4. Handling Outliers: About 8000 rows in Location attribute are (0,0) which is clearly an outlier. Since only 2.8% rows have outliers, these rows can either be dropped or marked as outliers and not include these while making any data interpretations related to location.

5. Converting datatype:  The date/time attributes namely, Dispatch Date Time', Start Date Time' and 'End Date Time' is converted to datetime datatype. Offence Code and CR Number is converted to String datatype as no numerical statistics can be derived from these. Latitude and Longitude is changed to float datatype in order to use them for location-based visualizations.

6. Fixing Errors: The above slice of data contains an error because the End Date Time is earlier than the Start Date Time, which is not possible. This most likely occurred when the crime's end time was extended into the early morning hours of the next day, but only the time was accurately recorded, and the date was not changed. In order to fix this error, the day component in End Date Time can be changed to next day for all the instances where End date time is before the Start Date Time.
   
7. Handling Inconsistent Records: Apart from the columns with abbreviations, all the entries are changed to correct case to ensure uniformity.

## Exploratory data analysis
Descriptive/Summary statistics (mean, median, standard deviation, etc.)
<img width="806" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/b0fc729f-11c2-42f0-a227-03f02590cfd4">

Frequency Histogram
<img width="812" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/712544ff-01f8-4683-a728-60fd6e1eddd0">

Correlation Map
<img width="812" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/7c6c4a83-d31e-4f25-bf5b-d9252263faf5">

##RESEARCH QUESTIONS ADDRESSED:
1. What kind of behaviour has the crime rates shown throughout the years? How do crimes stack up against one another when looking back over the previous five years?
2. What is the average response time of the police department? Response time is the period between when a crime is perpetrated or reported and when police are dispatched.
3. How long does criminal behaviour typically last? What region has the longest typical crime episode? How often do extended periods of increased crime occur?
4. Which area is the most and least dangerous? How has crime performed in these areas over the past five years? What sorts of crimes are often committed in the safest and most hazardous areas? How often do criminal acts occur in these regions?
5. What sort of location (e.g., streets, residences, grocery stores, etc.) has the highest and the lowest crime rate? What kind of crimes are being perpetrated in these regions? Which location is the constantly looking least hazardous to dwell in or reside near?
6. What kinds of streets are among the most susceptible to crime, and what kinds of crimes occur on the most hazardous streets? What are the most and least desirable times to commute on the street? What kind of crimes are committed along these streets?
7. What is the least desirable time to go out alone in the whole county? Additionally, when is the safest time to leave the house? How many potential victims are stuck at a
crime scene on average during these times?
8. When comparing crime figures from 2019 to 2020, what insights come into picture? How significant was COVID-19 in causing countywide crime trends to shift? Which part of the country had the biggest growth in safety, and which saw the most decline in security, over this phase?
