# Predicting The Next Hit Song Using Spotify Audio Features
![ImageCvr](img/coverart.png)

## Motivation:<br>
#### Can we predict what the next hit song will be? More specifically, can we identify "audio features" (from Spotify) of songs that characterize hit songs? <br>

The purpose of the project is to predict whether a song will make it to the Billboard Hot 100 Charts. This can help inform aspiring artists or producers in understanding these "audio feature" characteristics of popular hit songs. 

## Data:<br>
The data I used was publicly avaialble based on a previous research project. A link to the data:
* http://cs229.stanford.edu/proj2018/report/16.pdf<br>

The data is based on ~14,000 songs with a mix of billboard 100 songs and random songs from the Million Song Dataset:
* http://millionsongdataset.com/

I supplemented the data using Spotify's API with other Artist/Song attributes that were not originally provided - genre, track popularity, time signature, release year. I uploaded the data to a postgres-sql server and retreived for analysis.

## Features and Target Variables:<br>
The target variable consists of the songw that made it to the Billboard Hot 100 list between 1990-2018<br>
Features are mostly audio feature scores pulled from Spotify's API

## Programs:<br>
There are several programs for different models, however I focused mostly on logistic regression, random forest and XGB after the intial 
base model runs (00_base_models). I selected 07_xgb_mod_h100.ipynb as my primary model and program. I output a new analytic file with predictions and predicted probabilities to analyze the hits and misses. The program to analyze my predictions is in 99_investigations.

## Data Extract:<br>
* data_extract_bb_features.ipynb: this program uses song id info for billboard 100 songs and extracts features from Spotify's API<br>
* data_extract_sb_features.ipynb:  this program uses song id info for non-billboard 100 songs and extracts features from Spotify's API

## Data Housing and Cleaning:<br>
* *01_create_postgressql.ipynb:* Create the postgressql DB to house song data<br>
* *02_data_clean.ipynb:* Simple data frame cleaning

## EDA:<br>
* *02b_eda.ipynb:* EDA and graph production

## Models:<br>
* *02c_base_models.ipynb:* Run baseline models for all models prior to further exploration<br>
* *03_lr_mod_h100.ipynb:* Logistic regression modeling + tuning<br>
* *04_dt_mod_h100.ipynb:* Decision tree modeling<br>
* *05_rf_mod_h100.ipynb:* Random forest modeling + tuning<br>
* *06_knn_mod_h100.ipynb:* KNN modeling<br>
* *07_xgb_mod_h100.ipynb:* XGB modeling + tuning<br>
* *08_nb_mod_h100.ipynb:* Naive bayes modeling<br>
* *99_investigations.ipynb:* Final analysis of test data and predictions

## Summary:<br>
Based on EDA, model scores and evaluation metrics, I narrowed my focus on LR, RF and XGB models. 
XGB performed slightly better when looking at precision and recall and eventually decided to tune further.
Having raised my probability threshold to 0.65 to capture more precision, I ended up with a model with a precision of 0.84 and recall of 0.80.

The investigations program reviewed some positive, negative and edge cases of my predictions.
The model can be improved to incorporate more artist profile info vs. just audio features.
We may also benefit by looking at F1 beta scores vs. simply precision.
