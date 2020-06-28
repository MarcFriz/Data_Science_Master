# Data_Science_Master

## Data preparation
### First step - Process: Data_Preparation_Month_Year. See example process: [here](https://github.com/Tammy231/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/data_preparation_April2019.rmp)

- all single "day data" [here](https://github.com/Tammy231/Data_Science_Master/tree/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/04) 
of one month are appended to one csv file via "append" operator.
- Closed (3) and new (2) fuel stations are filtered out of the data set via operator "filter examples". 
- All data is sort by attributor "station_uuid" decreasing with the "sort" operator because empty data from fuel stations 
that have the same data as the day before, should be replaced with the data from the former day
-Replacement of data from former day by operator "replace missing value(series)" with setting: previous value
The results are too huge to share

### Second step A - merge the months for all stations, process: [here]

-Merge three month to one file with average price values with "Append operator"
-create a new date column because the original one consits of the time stamp and give the 
wrong average value when used as a key. This is done by the "Genrate Attributes" operator with function expression
"date_str_custom(date,"MMM d, yyyy")"
-get the average fuel prices of E5,E10 and Diesel with grouped by attribute "New Date" in the operator "Aggregate".
-Afterward, the operator "Nominal to Date" ist used to characterise the newly created date vfrom string to date format
to sort the date later correctly. 

The results can be found [here](https://github.com/Tammy231/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/PreparedQ2_2019_nolabel.rmhdf5table)

### Second step B - merge the months for one station

-Merge three month to one file with average price values with "Append operator"
-Use "filter examples" operator" to get only one station_unid. The chosen one ist from Stuttgart, Germany.
-create a new date column because the original one consits of the time stamp and give the 
wrong average value when used as a key. This is done by the "Genrate Attributes" operator with function expression
"date_str_custom(date,"MMM d, yyyy")"
-get the average fuel prices of E5,E10 and Diesel with grouped by attribute "New Date" in the operator "Aggregate".
-Afterward, the operator "Nominal to Date" ist used to characterise the newly created date vfrom string to date format
to sort the date later correctly. 

The results can be found [here](https://github.com/Tammy231/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/PreparedQ22019_nolabel_oneStation.rmhdf5table)

### Third step - Label the data

see next README for labeling