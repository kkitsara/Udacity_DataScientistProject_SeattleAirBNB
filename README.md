In this folder you may find the below files.

README.md - The file that explains the repository purpose and structure

LICENSE - The license file

DataScientistProject_Seattle.ipynb - It is the Jupyter Notebook that contains the analysis of the Seattle AirBNB data and the results.

DataScientistProject_Seattle_Functions.py - It is the python code that contains the definition of some functions used in Jupyter notebook. It should be imported in the notebook

AirBNBSeattleData.7z - The dataset of Seattle AirBNB data that are used for the project

AirBNBBostonData.7z - The dataset of Boston AirBNB data that are used for a comparison excercise

The project is built as part of Udacity Data Scientist course. 
Its purpose is to answer real life questions by analyzing data using the CRISP-DM methodology.

The dataset used is the AirBNB data of Seattle city and we try through this analysis to answer the below questions

Question 1: Is the Seattle a seasonal visit attraction?

Question 2: Are the cancellation policy, the reviews and the neighboorhood correlated with the booking count?

Question 3: Which are the key indicators of an listing price?

DataScientistProject_Seattle.ipynb
In the Jupyter Notebook you may find the below code:

1. The cell that imports the needed libraries. The imported libraries are:

pandas,numpy,sklearn,matplotlib,seaborn

Also we import a python code named DataScientistProject_Seattle_Functions

2. The code that reads the datasets that are included in the github repository

3. The code that performs checks and explores the data

4. The questions that we want to answer

5. The code that answers the question 1 by 1

Question 1 Methodology: In order to answer the 1st question "Is the Seattle a seasonal visit attraction?", we used the calendar.csv dataset and did aggregations in 
monthly level and in season level. Then we compared the results with the Boston datasets to check for differences.

Question 1 Result: It seems that some season's are most popular in Seattle (summer, winter) while in Boston it is quite opposite, as during spring and autumn there
are more bookings.

Question 2 Methodology: In order to answer this question "Are the cancellation policy, the reviews and the neighboorhood correlated with the booking count?" we 
introduced for each listing a new KPI the Bookings_Count from the calendar.csv dataset. After we joined this with the listings dataset, we did aggregations per 
cancellation policy, per reviews scores and per neighbourhood. All the data were normalized in order to have average bookings per appartment and not the total counts.

Question 2 Result: From the results we were in position to understand if there are correlations or not. The cancellation policy and the neighbourhood affect the 
average booking count per appartment, while the review scores seems to not be correlated.

Question 3 Methodology: In order to answer the 3rd question "Which are the key indicators of an listing price?", we build a linear regression model.
algorythm. First we run the linear model importing the full dataset as is, without removing any column. 

We used some standard methodologies to handle the numerical and the categorical attributes. Also we handled some more cases such as below:
A. We removed all the rows that do not have available the price value that we want to predict.
B. For the numerical we filled the empty values with the mean value.
C. For the categorical we created dummy attributes.
D. There were some numeric values such as the price that were stored as str in the dataset (eg. $85 value). We build a function in order to handle all these columns
and convert them to numeric (85.00)
E. There were some date columns that were handling as categorical ones. We build a function that converts them into numeric and the KPI changed to days until today.
For example if we had a date '2021-01-01' this values was converted to days_until_today => now()-'2021-01-01'. If today is 2021-04-18, the result is 108 days.

From the 1st run of the model, by using all the available columns, it was obvious that we should remove columns in order for the model to perform better.
We used several techniques in order to exclude columns:
1. We removed all the columns with variance more than 1000 and less than 3,
2. We removed all the columns that have 30% or more null values
3. We removed then manually some more columns based on testings and comon sense. For example it seems that the usage in the model of both attributes 
neighbourhood_group_cleansed and neighbourhood_group was confusing the model, while when using only one it worked better. Also some other columns with big variance
and/or not so related with the listings were removed, such as zipcode,host_location,smart_location were removed.

After performing the above steps and several tests we ended up with a model that was perofrming quite well and was in position to predict quite well the price.

4. As last step we run the cutoff and coefficient functions and we could see that by removing event further columns could benefit further the model. We proceeded
with the removal of the model of 2 columns that seems to had extremely high importance (edge) and indeed the removal seems to benefit the model. Then we removed
some more columns based on very low importance.

At the end the final model includes 133 variable with r square ~0.62.

Question 3 Result: It seems that the most important factors tha affect the price are the property type, the neighbourhood and the room type.

DataScientistProject_Seattle_Functions.py
In the code there are contained 2 functions that are used in the Jupyter notebook.
The 2 functions are:
find_optimal_lm_mod : Runs multipled tests of the X and y datasets and calculates different results in order to find the optimum linear model composition

coef_weights : Exports and depicts the coefficients of the linear model in order to undertand the importance of each variable.
