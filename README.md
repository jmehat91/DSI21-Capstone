# Predicting Lung Cancer Survival
-About

-Aim
## Hypothesis, Goals and Success Metrics
**Hypothesis**: Lung cancer survival can be predicted based on patient demographics, cancer details, and drugs received. 

**Goals**: 
1. Develop a classification model to accurately classify if a patient is alive or dead
2. Determine what features are important; eg. does ethnicity or do specific drugs impact survival?

**Success Metrics**:
1. Acheive an accuracy score above baseline 
2. Acheive a high precision score by reducing number of false positives; ie. predicting a patient is alive when they are actually dead


## Data Acquisition
The synthetic dataset, [The Simulacrum](https://simulacrum.healthdatainsight.org.uk/),  was easily downloaded in the form of a relational database containing 8 CSV files ranging from 0.5 million - > 2 million rows of patient data.

After opening a connection to a local SQLite database, the datasets were added and using SQL the relevant data were retreived and compiled into one dataset.

<img width="716" alt="Screenshot 2022-03-01 at 12 10 15" src="https://user-images.githubusercontent.com/41794055/156166876-461ad3c5-bcde-46ec-88e1-72acdee6b326.png">

## Data Cleaning and Feature Engineering
## Exploratory Data Analysis 
##### Eda blah blah
![image](https://user-images.githubusercontent.com/41794055/156353444-65729743-6bb3-4fd3-8905-333dddc563a6.png)
<img width="919" alt="Screenshot 2022-03-02 at 11 48 58" src="https://user-images.githubusercontent.com/41794055/156356281-846abbc9-dceb-4f82-8642-8708611d15c4.png">

##### something about age histogram

<img width="1046" alt="Screenshot 2022-03-02 at 11 42 12" src="https://user-images.githubusercontent.com/41794055/156355408-9bfcae04-32d0-4b9b-9ea6-8e26eff6f997.png">

## Modelling

### Features
<img width="467" alt="image" src="https://user-images.githubusercontent.com/41794055/156182128-2103e2a1-e5b3-4f86-a0ea-1493f5c93dec.png">

### Evaluation
<img width="399" alt="image" src="https://user-images.githubusercontent.com/41794055/156399864-a8fc8043-5ae4-416e-a0d9-35b658582e65.png">

