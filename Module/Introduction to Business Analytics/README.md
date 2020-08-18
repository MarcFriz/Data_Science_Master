# Data_Science_Master

## Introduction to Business Analytics

### Overview
This notebook will show the implementation for my presentation. Please keep in mind that this is just to show 
how the implementation could be done. There is no real value behind the thoughts for data preparation or real use 
model design.

#### Dependencies
- sklearn
- pandas
- numpy
- mlflow
- keras
- xgboost

### Usage
Install all requirements in your python environment and run the notebook.
#####  Dependencies
The easiest way to get the dependencies is to use pip. For example:
```
$ pip install pandas
```

### Dataset
The dataset will be the DATAMART you we have created during the praxis test in this module
You only have to create you .ini file with your credentials and edit the file in the notebook here:
```
config.read('C:/tmp/BI.ini')
```

### ML Flow
To start with mlflow, you have to navigate to the folder where the notebook is saved. If you had run
the notebook before there should be a folder named "mlruns". You can show all different runs and compare the metrics.
Type 
```
mlflow ui 
```
in your command-line interface and the mlflow server will be startet. After that you can access it via internet explorer.
 [http://localhost:5000/](http://localhost:5000/) 