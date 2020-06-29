# Data_Science_Master - exemplary for April 2019

See whole process [here]

## Data preparation fuel

### First step - Process:
- all single "day data" [here](https://github.com/Tammy231/Data_Science_Master/tree/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/04) 
of one month are appended to one csv file via "append" operator.
- Closed (3) and new (2) fuel stations are filtered out of the data set via operator "filter examples". 
- All data is sort by attributor "station_uuid" decreasing with the "sort" operator because empty data from fuel stations 
that have the same data as the day before, should be replaced with the data from the former day
- Replacement of data from former day by operator "replace missing value(series)" with setting: previous value


### Second step - merge the months for all stations

- Merge three month to one file with average price values with "Append operator"
- create a new date column because the original one consits of the time stamp and give the 
wrong average value when used as a key. This is done by the "Genrate Attributes" operator with function expression
"date_str_custom(date,"MMM d, yyyy")"
- get the average fuel prices of E5,E10 and Diesel with grouped by attribute "New Date" in the operator "Aggregate".
- Afterward, the operator "Nominal to Date" ist used to characterise the newly created date vfrom string to date format
to sort the date later correctly. 

## Data preparation Oil
### Third step - Joining different Oil Data in one file. 

- Joining the different oil data with the date as key. Important here to use the URALS Data set as join type as this data set consits of all dates from 
2018 and 2019 via the "Join" operator.

### Fourth step - Replace missing values

- Afterwards the missing price values are filled with "Replace missing values" operator und KNN method using ten k. 
- Both data sets URALS&BRENT and WTI are imputed with indiviual "Replace missing values" operators, as 
the missing year 2019 in the WTI data set interfere with the correct replacement of values in the URALS&BRENT data set. 


## Appending Fuel and Oil Data and Labelling them. 
See example process for all stations [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/Data_preparation_label.rmp)
and for only one station [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/Data_preparation_label_oneStation.rmp)

### Sixth step - Joining Fuel and Oil data:

- With "append" operator all "fuel-quarter files" are put in one fuel file 2018/2019
- with "Join" operator fuel and oil are joined to one file with the Date as key.

### Seventh step - labelling:

- With time series "Lag" operator, three new columns are created that consists of the former
day's fuel price by choosing the E5,E10 and diesel price columns as subset and adding the default lag "1".
- As for the first row (1.1.2018), there is no value, the "Replace missing values" operator is used
to replace the "?" with zero. --> This assumes a price increase for the first day of the year. 
- Then, the label columns have been created with the "generate attributes" function using the function
expression (example for E10): if([average(e10_cleaned)-1]>[average(e10_cleaned)],"0","1"). The formula indicates that
if the price of the former day in the new created row "average(e10_cleaned)-1" is higher than the current day, 
the label is "0" as no price increase took place. In case the former day value is lower, the label i "1"
as a price increase took place. 
- To see if the weekday is an important variable in the modell, the weekday is added by the "generate attributes"
operator using the functional expression "date_str_custom([Date New],"EEEE""
- For the final data set the "select attributes" operator is used to only get the relevant columns for the modelling
- As the data preparation process created a last row with only "?" values, this row is exluded by the "filter examples"
operator excluding all missing values.

# Data_Science_Master

## Data preparation fuel
### First step - Process: Data_Preparation_Month_Year. See example process: [here](https://github.com/Tammy231/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/data_preparation_April2019.rmp)

- all single "day data" [here](https://github.com/Tammy231/Data_Science_Master/tree/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/04) 
of one month are appended to one csv file via "append" operator.
- Closed (3) and new (2) fuel stations are filtered out of the data set via operator "filter examples". 
- All data is sort by attributor "station_uuid" decreasing with the "sort" operator because empty data from fuel stations 
that have the same data as the day before, should be replaced with the data from the former day
- Replacement of data from former day by operator "replace missing value(series)" with setting: previous value
The results are too huge to share

### Second step A - merge the months for all stations- See example process: [here](https://github.com/Tammy231/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/PreparedQ2_2019_noLabel.rmp)

- Merge three month to one file with average price values with "Append operator"
- create a new date column because the original one consits of the time stamp and give the 
wrong average value when used as a key. This is done by the "Genrate Attributes" operator with function expression
"date_str_custom(date,"MMM d, yyyy")"
- get the average fuel prices of E5,E10 and Diesel with grouped by attribute "New Date" in the operator "Aggregate".
- Afterward, the operator "Nominal to Date" ist used to characterise the newly created date vfrom string to date format
to sort the date later correctly. 

The results can be found [here](https://github.com/Tammy231/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/PreparedQ2_2019_nolabel.rmhdf5table)

### Second step B - merge the months for one station - See example process: [here](https://github.com/Tammy231/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/PreparedQ2_2019_noLabel_OneStation.rmp)

- Merge three month to one file with average price values with "Append operator"
- Use "filter examples" operator" to get only one station_unid. The chosen one ist from Stuttgart, Germany.
- create a new date column because the original one consits of the time stamp and give the 
wrong average value when used as a key. This is done by the "Genrate Attributes" operator with function expression
"date_str_custom(date,"MMM d, yyyy")"
- get the average fuel prices of E5,E10 and Diesel with grouped by attribute "New Date" in the operator "Aggregate".
- Afterward, the operator "Nominal to Date" ist used to characterise the newly created date vfrom string to date format
to sort the date later correctly. 

The results can be found [here](https://github.com/Tammy231/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/PreparedQ22019_nolabel_oneStation.rmhdf5table)

## Data preparation Oil
### Third step - Joining different Oil Data in one file. See example process [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/Oil_cleaning.rmp)

- Joining the different oil data with the date as key. Important here to use the URALS Data set as join type as this data set consits of all dates from 
2018 and 2019 via the "Join" operator.
- The WTI data set is separately considered because only the values for 2018 can be filtered with "filter example" operator and not 2019.
As some dates are missing, an extra process [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/Datumsstempel.rmp)
is created to also get each date of the year 2018.  

### Fourth step - Replace missing values

- Afterwards the missing price values are filled with "Replace missing values" operator und KNN method using ten k. 
- Both data sets URALS&BRENT and WTI are imputed with indiviual "Replace missing values" operators, as 
the missing year 2019 in the WTI data set interfere with the correct replacement of values in the URALS&BRENT data set. 

Results can be seen [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/Oil_Complete_Clean.csv)

## Appending Fuel and Oil Data and Labelling them. 
See example process for all stations [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/Data_preparation_label.rmp)
and for only one station [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/Data_preparation_label_oneStation.rmp)

### Sixth step - Joining Fuel and Oil data:

- With "append" operator all "fuel-quarter files" are put in one fuel file 2018/2019
- with "Join" operator fuel and oil are joined to one file with the Date as key.

### Seventh step - labelling:

- With time series "Lag" operator, three new columns are created that consists of the former
day's fuel price by choosing the E5,E10 and diesel price columns as subset and adding the default lag "1".
- As for the first row (1.1.2018), there is no value, the "Replace missing values" operator is used
to replace the "?" with zero. --> This assumes a price increase for the first day of the year. 
- Then, the label columns have been created with the "generate attributes" function using the function
expression (example for E10): if([average(e10_cleaned)-1]>[average(e10_cleaned)],"0","1"). The formula indicates that
if the price of the former day in the new created row "average(e10_cleaned)-1" is higher than the current day, 
the label is "0" as no price increase took place. In case the former day value is lower, the label i "1"
as a price increase took place. 
- To see if the weekday is an important variable in the modell, the weekday is added by the "generate attributes"
operator using the functional expression "date_str_custom([Date New],"EEEE""
- For the final data set the "select attributes" operator is used to only get the relevant columns for the modelling
- As the data preparation process created a last row with only "?" values, this row is exluded by the "filter examples"
operator excluding all missing values.

The final prepared data for all stations only April 2019 can be seen [here]

The final prepared data for only one station can be seen [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/cleaned/CleanedData_complete_oneStation.csv)


The final prepared data for all stations can be seen [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/cleaned/CleanedData_complete.csv)

The final prepared data for only one station can be seen [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/cleaned/CleanedData_complete_oneStation.csv)
