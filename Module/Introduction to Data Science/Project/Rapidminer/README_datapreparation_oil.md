# Data_Science_Master

## Data preparation Oil
### First step - Joining different Oil Data in one file. See example process [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/Oil_cleaning.rmp)

- Joining the different oil data with the date as key. Important here to use the URALS Data set as join type as this data set consits of all dates from 
2018 and 2019 via the "Join" operator.
- The WTI data set is separately considered because only the values for 2018 can be filtered with "filter example" operator and not 2019.
As some dates are missing, an extra process [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/process/preparation/Datumsstempel.rmp)
is created to also get each date of the year 2018.  

### Second step - Replace missing values

- Afterwards the missing price values are filled with "Replace missing values" operator und KNN method using ten k. 
- Both data sets URALS&BRENT and WTI are imputed with indiviual "Replace missing values" operators, as 
the missing year 2019 in the WTI data set interfere with the correct replacement of values in the URALS&BRENT data set. 

Results can be seen [here](https://github.com/MarcFriz/Data_Science_Master/blob/master/Module/Introduction%20to%20Data%20Science/Project/Rapidminer/daten/Oil_Complete_Clean.csv)

For appending fuel and oil data and labeling them, see README_Labeling.md [here]


