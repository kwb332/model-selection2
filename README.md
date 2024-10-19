
Overview of Project:

The goal of this project is to compare the performance of the following Classification models : 
K Nearest Neighbor (KNN), Logistic Regression, Decision Trees, and Support Vector Machines (SVM). The project utilizes a 
dataset related to marketing bank products over the telephone.  The data is from a a Portugese banking institution 
and is a collection of the results of multiple marketing campaigns. The business objective is to analyze the 
dataset of portuguese banks and its features to determine what features can be use to create the most optimal
 prediction model for predicting whether a patron will open a deposit account or not. In addition to determining 
 the most critical features, the business objective is to determine what 
model performs the best in predicting which patrons will open an account given the selected features.

Understanding the Data:

The dataset collected is related to 17 campaigns that occurred between May 2008 and November 2010, corresponding to a total of 79354 contacts. During these phone campaigns, an attractive long-term deposit application, with good interest rates, was offered. For each contact, a large number of attributes was stored and if there was a success 
(the target variable). For the whole database considered, there were 6499 successes (8% success rate).  The input and output variables are listed below:

Input variables:
# bank client data:
1 - age (numeric)
2 - job : type of job (categorical: 'admin.','blue-collar','entrepreneur','housemaid','management','retired','self-employed','services','student','technician','unemployed','unknown')
3 - marital : marital status (categorical: 'divorced','married','single','unknown'; note: 'divorced' means divorced or widowed)
4 - education (categorical: 'basic.4y','basic.6y','basic.9y','high.school','illiterate','professional.course','university.degree','unknown')
5 - default: has credit in default? (categorical: 'no','yes','unknown')
6 - housing: has housing loan? (categorical: 'no','yes','unknown')
7 - loan: has personal loan? (categorical: 'no','yes','unknown')
# related with the last contact of the current campaign:
8 - contact: contact communication type (categorical: 'cellular','telephone')
9 - month: last contact month of year (categorical: 'jan', 'feb', 'mar', ..., 'nov', 'dec')
10 - day_of_week: last contact day of the week (categorical: 'mon','tue','wed','thu','fri')
11 - duration: last contact duration, in seconds (numeric). Important note: this attribute highly affects the output target (e.g., if duration=0 then y='no'). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known. Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic predictive model.
# other attributes:
12 - campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)
13 - pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)
14 - previous: number of contacts performed before this campaign and for this client (numeric)
15 - poutcome: outcome of the previous marketing campaign (categorical: 'failure','nonexistent','success')
# social and economic context attributes
16 - emp.var.rate: employment variation rate - quarterly indicator (numeric)
17 - cons.price.idx: consumer price index - monthly indicator (numeric)
18 - cons.conf.idx: consumer confidence index - monthly indicator (numeric)
19 - euribor3m: euribor 3 month rate - daily indicator (numeric)
20 - nr.employed: number of employees - quarterly indicator (numeric)

Output variable (desired target):
21 - y - has the client subscribed a term deposit? (binary: 'yes','no')

The following steps were carried out to prepare the data for processing:

The Results field y was converted into a binary 1 for yes and 0 for no, so both categorical and numeric models can be used. 
The Education field was converted into an ordinal categorical field representing the degree of education. 
Marital status, job, loan and housing fields were converted using one hot encoding to make these categorical
fields numberic, this allowed for linear models and their derivatives to be used on this data. 
To ensure that the data consistent, "unknown" categories in each column were dropped. 
This allowed for more accurate comparison of features accross the data as unknowns are akin to nulls.

After the data was processes, a baselline model using linear regression with degree 2 polynomial was created.  This model
scored less than 25% in terms of accuracy.  Next KNN, Logistic Regression, SVM and Decision tree models were created without 
any fine tunning.  All four models were compared to each other using accuracy as the metric.

Finally, all the models in the previous step where optimized using Gridsearch and the results were compared to the corresponding
non-optimized models.


Evaluation of results:

For evaluating the models accuracy score and training speed is used.  This metric was chosen because it is a more consistent metric accross the different
models. However, an argument can be made for using recall instead, as there may be a business need to maximize the number
of people who take the banks deposit.

Results of Non-Optimized models

The results of the non optimized models show that, the Logistic Regression model had the best accuracy score, despite having the second slowest model training score. KNN 
was the fastest model but had the second lowest accuracy score (still very acceptable score of 87%).  Decision Tree model had
the second fastest training speed and highest training accuracy, but the lowest testing accuracy which means it may be a little
overfitted.  In conclusion, the best model for the Non-Optimized Models is Logistic Regression, because of its ability to be
adjusted to increase recall (using predict_proba) and because it has the highest accuracy.  There is however some concern with the training speed
of the Logistic Regression Model and so it may help to reduce the dimentionality and use regularization to improve training performance.
·
Results of Optimized models

The optimized models provided a different picture. The most accurate model was the SVM model although it had the second 
slowest training time.  Logistic regression had the slowest training time and its accuracy dropped slightly to third place. 
Decison Tree had the second highest accuracy, slighly below SVM, but had the fastest training time.  The Optimized 
Decision Tree model provided the best balance of Accuracy and Speed and so is the best overall Model for this project.


Next steps and recommendations

The next step, not included in this project is to reduce the dimentionality of the data to the subset of features determined
by the permutation importance algorithm that was ran during the project:

pdays   363.212 +/- 9.276
poutcome 275.424 +/- 3.732
euribor3m 27.159 +/- 0.219
previous 5.441 +/- 0.085
emp.var.rate 4.228 +/- 0.036
nr.employed 3.609 +/- 0.041
job     2.308 +/- 1.020
cons.conf.idx 0.242 +/- 0.007
cons.price.idx 0.108 +/- 0.004
campaign 0.015 +/- 0.003
age     0.008 +/- 0.001
education 0.006 +/- 0.001
marital 0.006 +/- 0.001
loan    0.004 +/- 0.001
housing 0.001 +/- 0.000

This subset of the data can be used to recreate the four models and compare them to each other.  Another next step would 
be to feed the new models into Gridsearch using a well selected set of hyper parameters to interate through.
All results and graphs that support the above findings can be seen in the attached Jupyter Notebook:  prompt_III-checkpoint.



