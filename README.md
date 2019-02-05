# EPL-Prediction-2019
EPL-Prediction-2019 is a mini project of Kathmandu University, Machine Learning COMP-484. This repo contains dataset, trained models, fixtures of EPL season 2018/2019 and IPython Notebook (ipynb) file.

## Team Members:
* [Binaya Kumar Chaudhary](https://binayachaudari.com.np/)
* [Prabish Kayastha](https://github.com/prabishkayastha)
* [Rojan Bade]()
* [Ujwal Lakhaju](https://github.com/ujwalbqcal)

## Dependencies
* scikit-learn
* pandas
* Seaborn
* glob
Install missing dependencies with [pip](https://pip.pypa.io/en/stable/).

## Dataset
The dataset contains data for last 10 seasons of English Premier League including current season. The data is updated on weekly basis via Travis-CI. The dataset is sourced from [DataHub](https://datahub.io/sports-data/english-premier-league) and contains various statistical data such as final and half time result, corners, yellow and red cards etc.

<p align="center">
  <img src="./img/dataset.png" alt="Dataset"
       width="590" height="539">
</p>

Dataset Field Information

<p align="center">
  <img src="./img/dataset_field_info.png" alt="Dataset Field Info"
       width="431" height="459">
</p>

## Data Visualization:
The plot below shows the total goals scored data, total shots on target data, total shots data and scoring ratio data distributed among teams. These data will be used in predicting win, loss and draw probability of each team.
These data were visualized using “Seaborn” library in python.

<p float="left">
  <img src="./img/Bar Diagrams/totalGoalsScored_vs_Teams.png" alt="Total Goals Scored vs TeamNames"
       width="441" height="330">
  <img src="./img/Bar Diagrams/totalShotsOnTarget_vs_Teams.png" alt="Total Shots on Target vs TeamNames"
        width="440" height="327">
  <img src="./img/Bar Diagrams/totalShots_vs_Teams.png" alt="Total Shots vs TeamNames"
        width="457" height="333">
  <img src="./img/Bar Diagrams/scoringRatio_vs_Teams.png" alt="Total Shots on Target vs TeamNames"
        width="417" height="334.5">
</p>


## Methodology
* Data Preprocessing:
After the dataset has been concatenated into a single file, only necessary features are kept into the dataset, unnecessary features such as Referee, Date, …, were dropped. There are some preprocessing steps which are done as the data get loaded into memory before training:
  * 10 csv files are concatenated into one csv file named “concat-season0119.csv”.
  *	Some unnecessary fields from the dataset were removed from the concatenated file. (‘Date’, ‘Referee’, ‘HTR’)
  *	New csv named “teams.csv” is created to know the teams that are playing in the league this (2018/2019) season.
  *	The FTR (Full Time Result) is our label which is to be predicted by the model, so we divided the data frames into two parts: feature set and target variable. All the other columns except FTR is features for training the model.
  *	Removed all the categorical variables that means all the categorical variables within the dataset is converted into dummy variables (numerical).

  For further preprocessing, following tools were used:
  i.	Sklearn train_test_split: used for cross validation, shuffle and split the dataset into training and testing data.


## Training and Evaluating models
* `Logistic Regression:`

```sh
Training a LogisticRegression using a training set size of 1448. . .
Trained model in 0.0319 seconds
Made predictions in 0.0064 seconds.
0.9932094854208314 0.994475138121547
F1 score and accuracy score for training set: 0.9932 , 0.9945.
Made predictions in 0.0011 seconds.
F1 score and accuracy score for test set: 1.0000 , 1.0000.
```

* `SVC:`

```sh
Training a SVC using a training set size of 1448. . .
Trained model in 0.1619 seconds
Made predictions in 0.0906 seconds.
0.953397350837176 0.9599447513812155
F1 score and accuracy score for training set: 0.9534 , 0.9599.
Made predictions in 0.0038 seconds.
F1 score and accuracy score for test set: 0.7407 , 0.7800.
```

* `KNeighborsClassifier:`

```sh
Training a KNeighborsClassifier using a training set size of 1448. . .
Trained model in 0.0052 seconds
Made predictions in 0.1366 seconds.
0.5075820056855057 0.6477900552486188
F1 score and accuracy score for training set: 0.5076 , 0.6478.
Made predictions in 0.0053 seconds.
F1 score and accuracy score for test set: 0.5156 , 0.6200.
```


## Conclusion
Even though the F1 score and accuracy for the training set is lower than the F1 score and accuracy of testing set, given the new data to model to classify with all features with value 0 (i.e. the game that has not been played has attributes like ‘FTAG’, ‘FTAG’, ‘HS’, ‘AS’ value 0) except for the Home Team name and the Away Team name, the trained model was able to predict future instances marginally better.
Any match is highly unpredictable and there are several other factors that come into play during a game. Players’ form, strategic nuances in formation, player injuries and fatigue level etc. constitute a major part of a team’s performance in a match. Data about such characteristics is not freely available. With more information about each match statistics in the dataset, the model might be able to accurately predict the future matches. Also implementing twitter sentiment analysis about each game, and the player statistics might increase the accuracy of the model. Including these features would help us get a better understanding of how to more accurately model the data available and also which factors contribute more to a team’s victory. Further research and analysis could be carried on by applying these models in other leagues and seasons.
