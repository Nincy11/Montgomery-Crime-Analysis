# MONTGOMERY CRIME ANALYSIS

<img width="664" alt="Screenshot 2023-12-25 at 6 41 58 pm" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/41fa8a12-1347-4d4a-8840-725f43eea06e">


## OVERVIEW OF DATASET
The dataset presents the crime details occurred in the Montgomery County in the state of Maryland in USA. It includes all founded crimes reported after July 1st, 2016, and are entered to-date utilizing Uniform Crime Reporting (UCR) rules. The dataset has the title ‘Crime’ and is acquired from Montgomery County’s open data website. It is open to public access and utilisation. The data is derived from the reported crimes classified according to the National Incident-Based Reporting System (NIBRS) of the Criminal Justice Information Services (CJIS) Division Uniform Crime Reporting (UCR) Program and documented by approved police incident reports. The dataset used for this experiment is real-time and is updated daily. The dataset is in a csv file with a structured format. The dataset is about 80 MB in size and consists of 317339 rows and 30 columns. A total of 291255 crimes with unique Incident ID have been reported in the dataset. It contains not only reported crimes but also attempted ones which are not further classified. Multiple offenses were reported for 26,084 crimes and each of these offenses may have multiple victims. The dataset also comprises of crimes that are not yet verified by further investigation.

## PRE-PROCESSING 

1. Dealing Missing values:<br>
<img width="452" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/3da25c65-ff0f-49fd-b431-85d82c525ff7">

Dropping the column: Street Prefix’ and ‘Street Suffix’ columns can be dropped since more than 95% of the entries are null and there is already pertinent information available describing the crime's location. 
Imputing values with Mean: About 50% of data in End Date Time’ is empty but these entries cannot be dropped as its crucial to calculate the duration of crime. Since the End Date Time cannot potentially exceed the time of the Police arrival, the empty entries in this column can be supplied with the matching Dispatch Date/Time values, if available. The remaining missing values in this field can be filled with the sum of average response time and Start Date Time. 

3. Removing Irrelevant data: The dataset can be made more intelligible and compact by filtering out the attributes that do not contribute anything useful to the understanding of the data. Hence, the below attributes are removed:
Incident ID, CR Number, Location, Police District Number, Block Address, Address Number, Zip Code, Sector/Beat/PRA.

4. Handling Outliers: About 8000 rows in Location attribute are (0,0) which is clearly an outlier. Since only 2.8% rows have outliers, these rows can either be dropped or marked as outliers and not include these while making any data interpretations related to location.

5. Converting datatype:  The date/time attributes namely, Dispatch Date Time', Start Date Time' and 'End Date Time' is converted to datetime datatype. Offence Code and CR Number is converted to String datatype as no numerical statistics can be derived from these. Latitude and Longitude is changed to float datatype in order to use them for location-based visualizations.

6. Fixing Errors: The above slice of data contains an error because the End Date Time is earlier than the Start Date Time, which is not possible. This most likely occurred when the crime's end time was extended into the early morning hours of the next day, but only the time was accurately recorded, and the date was not changed. In order to fix this error, the day component in End Date Time can be changed to next day for all the instances where End date time is before the Start Date Time.
   
7. Handling Inconsistent Records: Apart from the columns with abbreviations, all the entries are changed to correct case to ensure uniformity.

## EXPLORATORY DATA ANALYSIS
Descriptive/Summary statistics (mean, median, standard deviation, etc.)<br>
<img width="806" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/b0fc729f-11c2-42f0-a227-03f02590cfd4">

Frequency Histogram<br>
<img width="812" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/712544ff-01f8-4683-a728-60fd6e1eddd0">

Correlation Map<br>
<img width="812" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/7c6c4a83-d31e-4f25-bf5b-d9252263faf5">

## RESEARCH QUESTIONS ADDRESSED:
1. What kind of behaviour has the crime rates shown throughout the years? How do crimes stack up against one another when looking back over the previous five years?
2. What is the average response time of the police department? Response time is the period between when a crime is perpetrated or reported and when police are dispatched.
3. How long does criminal behaviour typically last? What region has the longest typical crime episode? How often do extended periods of increased crime occur?
4. Which area is the most and least dangerous? How has crime performed in these areas over the past five years? What sorts of crimes are often committed in the safest and most hazardous areas? How often do criminal acts occur in these regions?
5. What sort of location (e.g., streets, residences, grocery stores, etc.) has the highest and the lowest crime rate? What kind of crimes are being perpetrated in these regions? Which location is the constantly looking least hazardous to dwell in or reside near?
6. What kinds of streets are among the most susceptible to crime, and what kinds of crimes occur on the most hazardous streets? What are the most and least desirable times to commute on the street? What kind of crimes are committed along these streets?
7. What is the least desirable time to go out alone in the whole county? Additionally, when is the safest time to leave the house? How many potential victims are stuck at a
crime scene on average during these times?
8. When comparing crime figures from 2019 to 2020, what insights come into picture? How significant was COVID-19 in causing countywide crime trends to shift? Which part of the country had the biggest growth in safety, and which saw the most decline in security, over this phase?


1. What kind of behaviour has the crime rates shown throughout the years? How do crimes stack up against one another when looking back over the previous five years? 
Upon analysing the data and visualising it, we found the trend of crimes rising during the start, but then the rate of crime starts to recede after 2017 to 2022.  <br>
<img width="452" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/d8685439-52ad-462e-b044-2888034c29c3">

The percentage of crimes across the dataset, when broken down by year, shows that crimes are almost evenly distributed, with a much lower proportion before and post the pandemic. <br>
<img width="265" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/cf41c144-7f59-405f-8f74-68672ec9a136">
 
2. What is the average response time of the police department? Response time is the period between when a crime is perpetrated or reported and when police are dispatched. 
Statistics show that, apart from MCSO and P, all other agencies had appropriate response times to crimes, with MCFM being the fastest to react in 16 seconds and RCPD being the slowest calls in 1 minute and 12 seconds. The agency with the most crime reports, MCPD, has a response time of 51 seconds, which is the second worst but still fast enough.<br>
<img width="452" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/124cceda-f778-4c2f-8f2b-0825515d5e2a">
 
4. Which area is the most and least dangerous? How has crime performed in these areas over the past five years? What sorts of crimes are often committed in the safest and most hazardous areas? How often do criminal acts occur in these regions?  
Upon crunching statistics to examine the most and the least hazardous regions around the county, we notice that Silver Spring is the most dangerous and Takoma Park is the least dangerous. But again, after calculating the percentages of instances that each region gets, it becomes obvious that there is a direct association between the size of the area and the number of cases received. <br>
![image](https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/cce480b7-fc6a-48cb-8e59-2f2a3a601d62)
 
5. What sort of location (e.g., streets, residences, grocery stores, etc.) has the highest and the lowest crime rate? What kind of crimes are being perpetrated in these regions? Which location is the constantly looking least hazardous to dwell in or reside near? 
Upon analysing the data, we can conclude that most of the crimes perpetrated throughout the last 5 years are on either streets or residential areas. With more than 40% crimes committed being distributed amongst these regions. The reason for choosing the number of victims to be greater than 20000 is that we want only those places which are unsafe. 
 <br>
![image](https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/bf61ba11-c8a3-4ba1-b7a6-928a89eb855a)
(Bar graph of the least safe locations in descending order) 

6. What kinds of streets are among the most susceptible to crime, and what kinds of crimes occur on the most hazardous streets? What are the most and least desirable times to commute on the street? What kind of crimes are committed along these streets? 
The most dangerous streets in Maryland are Georgia and Frederick, with 13803 and 9129 criminal acts, respectively. There is a significant difference in these data, indicating that Georgia Street has been the most dangerous throughout the years. In contrast, Montgomery has had little more than 1200 crimes throughout the years, making it one of the safest streets in Maryland. <br>
<img width="457" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/8ff5dfc9-c827-4ab8-b5f5-6c908b4e1bdb">
(Bar graph of the most unsafe street) 
 
  
7. What is the least desirable time to go out alone in the whole county? Additionally, when is the safest time to leave the house? How many potential victims are stuck at a crime scene on average during these times?   
After a substantial amount of analysis, it was evident by the number of crimes perpetrated from noon to night was almost twice the number of offenses perpetrated from midnight to noon. <br>
  
<img width="390" alt="image" src="https://github.com/Nincy11/Montgomery-Crime-Analysis/assets/46756664/ca33b203-a766-4d6d-ada1-a10260ec3815">
(Times where crime peaks) 
 
8. When comparing crime figures from 2019 to 2020, what insights come into picture? How significant was COVID-19 in causing countywide crime trends to shift? Which part of the country had the biggest growth in safety, and which saw the most decline in security, over this phase? 
By combining the data and comparing it to the number of crimes committed before and after the pandemic, we can observe that 60% of the crimes were committed prior to COVID, which, when averaged, results in 15% of crimes every year. In comparison, over 40 percent of crimes were committed during and after the epidemic, or an average of 13.3 percent every year. The crime rates have decreased from prepandemic to post-pandemic, as previously determined statistically. 
 	 
##CONCLUSION 
The dataset supplied a wealth of insights, however we were required to spend a great deal of time curating and cleaning the data to meet our requirements. Regarding timestamps, there were several inconsistencies. We needed to standardise the time data for it to meet our needs. We were compelled to eliminate almost nine columns since they were irrelevant to the analysis that was to be conducted. Additionally, we had to synthesis many columns to get data and insights from them. To guarantee that only non-essential data and columns were removed and that null values were handled effectively, the first data analysis required much brainstorming. Exploratory data analysis revealed a new universe of opportunities. We addressed correlation, determined which columns are strongly associated, and used them for most of the EDA. We saw peculiar tendencies and correlational patterns that made sense. 
Using data visualisation tools, a whole new viewpoint on data became apparent. With matplotlib and seaborn, everything was difficult to grasp with statistics and number crunching got simplified. Many significant insights were generated from the data that were not apparent from the data alone, making it simpler to spot trends and discern patterns. 
