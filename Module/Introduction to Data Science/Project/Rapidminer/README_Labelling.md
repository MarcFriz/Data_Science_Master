# Data_Science_Master

## Appending Fuel and Oil Data and Labelling them. See example process for all stations [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/Data_preparation_label.rmp)
and for only one station [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/Data_preparation_label_oneStation.rmp)

### First step - Joining Fuel and Oil data:

- With "append" operator all "fuel-quarter files" are put in one fuel file 2018/2019
- with "Join" operator fuel and oil are joined to one file with the Date as key.

### Second step - labelling:

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

The final prepared data for all stations can be seen [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/cleaned/CleanedData_complete.csv)
The final prepared data for only one station can be seen [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/cleaned/CleanedData_complete_oneStation.csv)

