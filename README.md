# Activity_Prediction
Predicts Activities based on Sensor Measurement. Dataset used for Modelling is the PAMAP3 Dataset

- #**ABSTRACT**

The main aim of this report is to develop actionable insights which can help predict the type of physical activity carried out by an individual depending on the heart rate and the duration of activity. Application can be seen in real-life scenario where subjects use wearable technologies such as smartwatches which record user movement.

To carry out this research, The PAMAP2 Physical Activity Monitoring dataset was used. The dataset consists 9 subjects participating in 12 different physical activities including: lying, sitting, standing, walking, running, cycling, Nordic walking, watching TV, computer work, car driving, ascending stairs, descending stairs, vacuum cleaning, ironing,folding laundry, house cleaning, playing soccer, rope jumping and other transient activities.

The multivariate nature of the data was compressed by the use of dimensisonality reduction. Dimensionality reduction was performed with the sklearn.decomp library and two techniques were used to model this system.

The Two techniques used to model this dataset include a supervised learning technique which is the logistic regression and the unsupervised learning technique which is the K-Means clustering.

The main finding from the data exploration is that the heart rate and the duration of activities are not sufficient to accurately predict the physical activity being performed, only in partnership with other sensory measurements can predictions be made to a level of certainty.

Recommendations include increased sensory measurements, height measurements and distance measurements to improve the predictive accuracy of the models.


 **INTRODUCTION**

The objective of this report is to gain actionable insights from the PAMAP2 dataset, which helps in determining the amount and type of physical activity carried out by an individual. The PAMAP2 Protocol dataset is a labelled dataset obtained from 9 subjects of different demographics.

The type of physical activity which can be predicted is restricted to : lying, sitting, standing, walking, running, cycling, Nordic walking, watching TV, computer work, car driving, ascending stairs, descending stairs, vacuum cleaning, ironing,folding laundry, house cleaning, playing soccer, rope jumping.

Insights from this analysis will inform our design process for the development of hardware/software which can carry out this prediction to a satisfactory level of certainty.

 **LITERATURE REVIEW**

- **Data Collection**

Inertial measurement units were collected with 3 Colibri wireless IMUs with a sampling frequency of 100Hz positioned over the wrist of the dominant arm, on the chest, and on the dominant side of the ankle.

Heart rate readings were taken with the HR monitor: BM-CS5SR from BM innovations GmbH with a sampling frequency of 9Hz.

9 subjects including 1 female and 8 males aged between 23-30 years with a BMI between 22kgm-2 and 27kgm-2 performed 12 different activities(lying, sitting, standing, walking, running, cycling, Nordic walking, watching TV, computer work, car driving, ascending stairs, descending stairs, vacuum cleaning, ironing,folding laundry, house cleaning, playing soccer, rope jumping.). The activityID was labelled through a GUI running on the Viliv S5 UMPC.

Missing data occuring in the dataset are due to problems with hardware setup, and a frequency mismatch between Colibri wireless IMUs which takes readings every 0.01s and the heart rate monitor which takes readings every 0.1s. There was also a rare case of data dropping due to the wireless sensors.

  - **Data Format**

The initial unwrangled,labelled data from all the subjects representing metrics such as the timestamp,activity ID, heart rate and various IMU sensory data for the hand,chest and ankle is combined into 1 data file per subject per session,as text-files.

This dataset enables us to formulate a model which  predicts the physical activiity a subject has engaged in to a level of certainty.

**METHODS**

  - **Data preprocessing**

Each entry in a file was opened, cleaned and partitioned before being ultimately appended to one list. The need for preprocessing can not be overemphasized. Because this dataset is a raw text file, it contains tokens which have to be removed before analysis can take place. Tokens such as '\n' present in the file were replaced with "," using a custom regex definiton.

Noting that each line in a file is an entry for a particular event. The line was partitioned into 54 individual elements using a .split(" ") command. The output of this preprocessing step for all files is a list of lists which can be easily read into a dataframe using a pandas library.

The pandas library is used to convert this file into a dataframe, with the appropriate columns named and included. This aids data exploration and analysis.

Before analysis and exploration, the entries to the dataframe were cleaned .All NaN values are removed, and the data types of each column were converted to a float type. Transient activities with activity ID of 0 are also excluded from analysis.

  - **Data Splitting**

The dataset was shuffled for randomization and further split into a train set and test set in the ratio 70:30 . The reason for this is to prevent overfitting/underfitting and to also have a portion of the dataset to evaluate the accuracy of the models created.

A 'duration' column created from the timestamps to account for the time of each activity was added to the dataframe. 

  - **Exploratory Data Analysis**

Exploratory Data Analysis carried out includes: 

i) The correlation between the each of the measurement taken per event was investigated. This is the same as making a correlation plot between the columns  of the dataframe and displayed with a seaborn heatmap.

ii) The distribution of the heart rates within subjects per activity. This was obtained using a boxplot and displayed with a facetGrid.

iii)The density and count distribution of heart rate. This was displayed with a histogram and a kernel density plot.

iv)Mean heart rate across activities to examine trend by activity. This was displayed with a bar plot.

v)Total duration across activities to examine trend by activity. This was displayed with a bar plot.

vi)The Inertial Measurement Units(IMU) for the hand across activities to examine trend by activity. This was displayed with a bar plot.

vii)The inertial Measure Units (IMU) for the chest across activities to examine trend by activity. This was displayed with a bar plot.

viii)The inertial Measure Units (IMU) for the ankle across activities to examine trend by activity. This was displayed with a bar plot.

x) The range of distribution of the heart rate across activity IDs. This was displayed with a scatterplot. 

x) The nature of the relationship between the heart rate and the activity ID. This was done using a regression plot with various orders.

- **Hypothesis Testing**

The hypotheses tested includes:

- the relationship between heart rate and the duration of activities performed.

- the relationship between the duration and activities performed.

**Modelling**

i) XGBoost: XGboost is a tabular modelling algorithm which achieves state of art on tabular data. Inherent in its algorithm, it handles missing data, imbalanced classes accurately with little need for upsampling and imputation. It also achieves the best result on the PAMAP3 Dataset

ii) Dimensionality reduction

Dimensionality reduction is used to reduce the features representing an object of interest. The benefit includes faster computational time with less features to compute while still retaining correlation between features. A decomposed dataset gives a broad outlook on the relationship between dependent variable and independent variables.

In this case, we have several columns of different measurements which measures the state of a subject while performing an activity. Dimensionality reduction of both the train set and test set was performed using the sklearn.decomp library. Both sets of data were decomposed into two principal components

The activity ID's of the test and train set were ignored during decomposition because it is the dependant variable  being investigated with other independent variable, including it skews the data.

iii) Logistic Regression

Logistic Regression is a supervised learning method. This model is a form of predictive analysis used to predict future data based on old data. In this case, it helps solve the problem of classification of activities based on sensory measurements such as the heart rate, duration.With the aim of finding a predicted activity from these meaasurements, a Logistic Regression model from a sklearn.linear_model library was initialised, fitted and transformed with the decomposed train set data

Model training occurs on the train set. To prevent overfitting/underfitting, multiple models were created and the respective model score evaluated.


iv) Clustering

In addition to logistic regression, another model was created to predict activities based on the heart rate and duration of activities.This model employs an unsupervised approach.

Gaining insights from using an unsupervised approach can be done with various methods. The method used in this research is Clustering. As Clustering is  performed on unsupervised dataset, all labels(activityID) were dropped. K-means Clustering was performed and the choice  of this technique was informed by the fact that the number of clusters- equal to the number of physical activities, is already known. Since the number of clusters is already predetermined, K-Means Clustering is preferred over Aggregated clustering. K-Means reduces the computational overhead compared to Aggregated clustering.

The quality of the clustering obtained was evaluated independently using the silhouette score. The silhouette score measures how well each data point has been classified, with a score ranging from -1 to 1. A score of +1 means samples have been assigned to the right clusters, while a score of -1 means samples have been assigned to the wrong clusters

A K-means model was initialised with 12 clusters, fitted and transformed with the decomposed train  set data. This model was then tested on the corresponding decomposed test set data to predict the probable activityID of each event in the test set. The results obtained from the model however is of a different set of values compared to the activity ID's. To solve this problem, a function was created to interpolate the values to match the set of values of the activity ID. This step is a necessary one before the evaluation of the accuracy of the K-means model.

iv) Model Selection

The accuracy and confusion matrix of the models created are compared to assess the preferred model. XGBoost provided the highest accuracy on the test set with 97.6%
