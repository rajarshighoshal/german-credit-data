## German Credit Analysis from https://archive.ics.uci.edu/ml/datasets/Statlog+%28German+Credit+Data%29

The traget of the analysis is to classify customers as good or bad based on attributes given ionm the dataset by creating a classification model.

### Description of the German credit dataset.

1. Title: German Credit data

2. Source Information

Professor Dr. Hans Hofmann  
Institut f"ur Statistik und "Okonometrie  
Universit"at Hamburg  
FB Wirtschaftswissenschaften  
Von-Melle-Park 5    
2000 Hamburg 13 

3. Number of Instances:  1000

Two datasets are provided.  the original dataset, in the form provided
by Prof. Hofmann, contains categorical/symbolic attributes and
is in the file "german.data".   
 
For algorithms that need numerical attributes, Strathclyde University 
produced the file "german.data-numeric".  This file has been edited 
and several indicator variables added to make it suitable for 
algorithms which cannot cope with categorical variables.   Several
attributes that are ordered categorical (such as attribute 17) have
been coded as integer.    This was the form used by StatLog.


6. Number of Attributes german: 20 (7 numerical, 13 categorical)
   Number of Attributes german.numer: 24 (24 numerical)


7.  Attribute description for german

Attribute 1:  (qualitative)
	       Status of existing checking account
               A11 :      ... <    0 DM
	       A12 : 0 <= ... <  200 DM
	       A13 :      ... >= 200 DM /
		     salary assignments for at least 1 year
               A14 : no checking account

Attribute 2:  (numerical)
	      Duration in month

Attribute 3:  (qualitative)
	      Credit history
	      A30 : no credits taken/
		    all credits paid back duly
              A31 : all credits at this bank paid back duly
	      A32 : existing credits paid back duly till now
              A33 : delay in paying off in the past
	      A34 : critical account/
		    other credits existing (not at this bank)

Attribute 4:  (qualitative)
	      Purpose
	      A40 : car (new)
	      A41 : car (used)
	      A42 : furniture/equipment
	      A43 : radio/television
	      A44 : domestic appliances
	      A45 : repairs
	      A46 : education
	      A47 : (vacation - does not exist?)
	      A48 : retraining
	      A49 : business
	      A410 : others

Attribute 5:  (numerical)
	      Credit amount

Attibute 6:  (qualitative)
	      Savings account/bonds
	      A61 :          ... <  100 DM
	      A62 :   100 <= ... <  500 DM
	      A63 :   500 <= ... < 1000 DM
	      A64 :          .. >= 1000 DM
              A65 :   unknown/ no savings account

Attribute 7:  (qualitative)
	      Present employment since
	      A71 : unemployed
	      A72 :       ... < 1 year
	      A73 : 1  <= ... < 4 years  
	      A74 : 4  <= ... < 7 years
	      A75 :       .. >= 7 years

Attribute 8:  (numerical)
	      Installment rate in percentage of disposable income

Attribute 9:  (qualitative)
	      Personal status and sex
	      A91 : male   : divorced/separated
	      A92 : female : divorced/separated/married
              A93 : male   : single
	      A94 : male   : married/widowed
	      A95 : female : single

Attribute 10: (qualitative)
	      Other debtors / guarantors
	      A101 : none
	      A102 : co-applicant
	      A103 : guarantor

Attribute 11: (numerical)
	      Present residence since

Attribute 12: (qualitative)
	      Property
	      A121 : real estate
	      A122 : if not A121 : building society savings agreement/
				   life insurance
              A123 : if not A121/A122 : car or other, not in attribute 6
	      A124 : unknown / no property

Attribute 13: (numerical)
	      Age in years

Attribute 14: (qualitative)
	      Other installment plans 
	      A141 : bank
	      A142 : stores
	      A143 : none

Attribute 15: (qualitative)
	      Housing
	      A151 : rent
	      A152 : own
	      A153 : for free

Attribute 16: (numerical)
              Number of existing credits at this bank

Attribute 17: (qualitative)
	      Job
	      A171 : unemployed/ unskilled  - non-resident
	      A172 : unskilled - resident
	      A173 : skilled employee / official
	      A174 : management/ self-employed/
		     highly qualified employee/ officer

Attribute 18: (numerical)
	      Number of people being liable to provide maintenance for

Attribute 19: (qualitative)
	      Telephone
	      A191 : none
	      A192 : yes, registered under the customers name

Attribute 20: (qualitative)
	      foreign worker
	      A201 : yes
	      A202 : no



8.  Cost Matrix

This dataset requires use of a cost matrix (see below)


      1        2
----------------------------
  1   0        1
-----------------------
  2   5        0

(1 = Good,  2 = Bad)

the rows represent the actual classification and the columns
the predicted classification.

It is worse to class a customer as good when they are bad (5), 
than it is to class a customer as bad when they are good (1).



### Cleaning the data
I am using _credit.data_ file for the analysis. After loading the file into environment the column names are changed to more appropriate names for better understanding and easier analysis. After that cconverted (1,2) to (0,1) in the columns for easier analysis. Then check for NA values, as there is none, no imputaion is reuired. 

### Plotting univariate graphs
Plotting variables to gain overall idea about them. Also, cleaning numerical variable with outliers.

### Plotting some bivarite analysis
Doing some bivariate analysis and plotting them to gain idea about interdependence about hose variables.


### Model creation
I decided to create model using general linear model. 
For general linear model as variables are not in much diverse range except 2/3 variable so I decided scaling is not required. However this may have effected the model so it needs to be addressed in future evaluation.

#### Cost matrix
As per the instruction in the given dataset I am using the following cost matrix to estimate the cost of prediction.
      1        2

  1   0        1

  2   5        0

(1 = Good,  2 = Bad)

#### General linear model
For general linear model I kept all the variables in numerical format and split the data and 70% and 30% ratio for training and testing purpose respectively.
**Step-1**
Create model with all other features vs classification and look at the summary.
**Step-2**
Step wise reduce AIC using stepAIC function from MASS package and store it in a variable. 
**Step-3**
Call the formula predicted by stepAIC to bulid next model. View the summary and vif of the model.
**Step-4**
Remove variable with highest vif and not much significant p-value and create a model with the new variables. At each point remove only one variable and check summary and vif. After all the variable are having less than 2 vif stop checking for vif anymore.
**Step-5**
After that start looking at varibale with high p-value and remove one at a time and  check summary. Contin ue to do so until all the variables have low p-value and/or number of variables are low.
**Step-6**
Build the final model based on the variable with low p-values and low vif.
**Step-7**
After that predict classification values of test data set. Use a cutoff of 0.5 to predict as the model gives only probability values. So, values greater than equal to 0.5 should be predicted as 1 i.e. prone to default and values lower than 0.5 shoulds be predicted as 0 i.e. not prone to default. 
**cost calculation**
After that create a confusion matridx showing values of predicted and actual values with false-positive + true-positive + true-negative + false-negative. Then Mutliply that confusion matrix with the cost matrix appropriately to get the cost of the model i.e. what is the cost for predicting using the model.

### Predicting all the values
After the final model creation just get all the predictions and append them in a column.
