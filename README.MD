# Predicting Student Test Scores
Here is the code I used to complete the "Predicting Student Test Scores | Playground Series - Season 6 Episode 1" challenge on Kaggle. 
This is my first time participating in this type of challenge.

## My approach

### Models 
For this challenge, I started with only XGBoost. Then I added CatBoost and LightGBM to improve performance. 
The three models don't have the same impact on the final result. I created a weighted average where XGBoost contributes 60% to the final score, LightGBM 30%, and CatBoost 10%. I chose these weights based on my experiments and the results obtained with Optuna.

### Optuna
I used Optuna to find the optimal parameters for my models. The code using Optuna is available in the notebooks, but it's possible to train the models to generate predictions without using the Optuna blocks because I directly hardcode my parameters. This allows you to start training and generate predictions quickly, without waiting for the optimization process to finish.

### Mean vs K-Fold
You will find two similar notebooks in the repository, corresponding to my two final submissions. They differ in how they handle text columns (strings) by replacing them with numbers.

* `optuna-mean.ipynb` (The mean version): This version calculates the average of the final grades for each category using the entire dataset. It means the model slightly "knows" the answer for the current student because their grade is included in the average. It is risky, but it gave me the best score on the public leaderboard.

* `optuna-kfold.ipynb` (The "K-Fold" version):
  This version splits the dataset into 20 folds. To calculate the average for a group, it uses the other 19 folds (which represents 95% of the dataset).