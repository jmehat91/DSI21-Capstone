# Predicting Lung Cancer Survival

Lung cancer is the third most common cancer in both the US and UK, however, it is the number 1 cause of cancer death in these countries. While lifestyle factors, such as smoking, contribute heavily to the development of the disease, there are many other factors that influence whether a patient will survive or not once diagnosed. These factors may include patients’ age and ethnicity, the stage and other clinical factors of the cancer, and the specific drugs received to treat the cancer. Determining what factors impact survival could help improve patient diagnoses and determine better treatment options.   

## Hypothesis, Goals and Success Metrics
**Hypothesis**: Lung cancer survival can be predicted based on patient demographics, cancer details, and drugs received. 

**Goals**: 
1. Develop a classification model to accurately classify if a patient is alive or dead
2. Determine what features are important; eg. does ethnicity or do specific drugs impact survival?

**Success Metrics**:
1. Acheive an accuracy score above baseline 
2. Acheive a high precision score by reducing number of false positives; ie. predicting a patient is alive when they are actually dead


## Data Acquisition
Public Health England’s National Cancer Registration and Analysis Service (NCRAS), is one of the most comprehensive databases on cancer and tumour diseases. Every year, the NCRAS collects information on > 300,000 cases of cancer, including patient details (name, address, age, sex, ethnicity, etc.), detailed data about the type of cancer, how advanced it is and the drugs the patient received. In order to protect the anonymity of the patients while still using the database for research purposes, a synthetic dataset, known as the [The Simulacrum](https://simulacrum.healthdatainsight.org.uk/), was created which accurately mimics the real database.      

The Simulacrum, was downloaded in the form of a relational database containing 8 CSV files ranging from 0.5 million - > 2 million rows of patient data.

After opening a connection to a local SQLite database, the datasets were added and using SQL the relevant data were retrieved and compiled into one dataset to work with. 

<img width="716" alt="Screenshot 2022-03-01 at 12 10 15" src="https://user-images.githubusercontent.com/41794055/156166876-461ad3c5-bcde-46ec-88e1-72acdee6b326.png">

## Data Cleaning and Feature Engineering
### Cleaning:
The main data cleaning steps involved the following:
- Identifying variables relevant to modelling, and which to drop.
- Interpreting continuous and categorical features.
- Creating more model-friendly feature names.
- Exploring opportunities for new feature creation.
- Looking for and removing features with a high number of missing data.
- Changing the target variable to binary values (0 = dead; 1= alive)

### Feature engineering:

Once the new dataset was formed there were duplicates of the patient ID rows due to patients receiving more than 1 drug. The drug column was therefore dummified and then each drug aggregated to patient ID.

Final features included:
- Patient age
- Patient ethnicity
- Patient income deprivation level
- Lung cancer type
- Cancer stage 
- Cancer histology
- 227 different drugs / columns 

## Exploratory Data Analysis 

Exploring the distribution of the target variable highlighted the class imbalance between the number of alive (29%) vs dead (71%) patients. 

![image](https://user-images.githubusercontent.com/41794055/156353444-65729743-6bb3-4fd3-8905-333dddc563a6.png)


There was no difference in patient age between the dead and alive classes. The median age of patients was ~70 years old and examining the boxplot for outliers, led me to remove patients under the age of 20 years as it would be unlikely for patients that young to be diagnosed.

<img width="919" alt="Screenshot 2022-03-02 at 11 48 58" src="https://user-images.githubusercontent.com/41794055/156356281-846abbc9-dceb-4f82-8642-8708611d15c4.png">


Exploring some of the distribution of the different drugs received or not received by the alive and dead classes highlighted that while some of the more common/wide ranging drugs/chemotherapies (steroids and carboplatin) were received by a high number of both alive and dead patients, some new more target drugs (pembrolizumab) were received by few patients, both dead or alive. 

<img width="1046" alt="Screenshot 2022-03-02 at 11 42 12" src="https://user-images.githubusercontent.com/41794055/156355408-9bfcae04-32d0-4b9b-9ea6-8e26eff6f997.png">

## Modelling

The steps included:
- Data was standardised using a StandardScaler.
- Categorical data was dummified. 
- Data was treated with SMOTE to even out class imbalance; or without.
- The data was divided into train and test splits (80:20) and fed into classification models.

### Results

<img width="499" alt="Screenshot 2022-03-09 at 15 12 33" src="https://user-images.githubusercontent.com/41794055/158358207-a04669ff-7722-4fca-adcf-fd6b438e8a25.png">

The XGBoost on both the balanced and imbalanced data resulted in the highest accuracy scores. 

### Evaluation - Accuracy and Precision 
*Accuracy = # correct alive and dead predictions / total # predictions* 

The XGBoost model on the balanced data resulted in an accuracy score of 81.4%.

*Precision = # correct alive predictions / # correct alive+false alive predictions* 

The precision score for the alive class was 65%.

A high precision score desired for this project. This was because we wanted to reduce the number of false positive predictions, ie. predicting a patient is alive when they are actually dead. 

The ROC curve indicates a threshold of 0.7 results in an optimal precision score (78%). 

 ![image](https://user-images.githubusercontent.com/41794055/158358391-f727e121-fc57-4d8d-9461-2425994fa277.png)

### Features
The top features of importance included: age, cancer stage, and several chemotherapy drugs.
 ![image](https://user-images.githubusercontent.com/41794055/158358487-52ebeb94-7570-41a9-a0c5-1f95824c906a.png)
 
 ## Limitations

- Although SMOTE was used to address the class imbalance in the target variable, other methods, such as ADYSON, could have also been implemented and may have resulted in different accuracy/precision scores. 
- There was an assumption that the features did not have multicollinearity.
- There may have been features included in the analysis that were not relevant, specifically the drug variables - there was a high number of different drugs and certain drugs may have been received by very few patients

## Future Work
- Using a grid search to tune a decision tree model and visualise the tree to better determine the features involved in the decision and what class is impacted.
- Grouping the individual drugs under drug classes or mechanism of action, which may reduce the noise of including all drugs separately.
- Explore different cancer types to examine trends in the alive and dead class as well as determine if other predictors, ie. drugs, are more or less important.




