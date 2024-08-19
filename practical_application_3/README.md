# Bank Marketing Campaign Analysis
We assessed four classification models (Logistic Regression, K-Nearest Neighbors, Decision Tree, and Support Vector Machine) on a Portuguese bank marketing campaign dataset to predict the success of marketing efforts. Each model was optimized for best parameters, and their performance was evaluated based on train and test accuracy, precision, and computational time.

### Business objective
The main goal of this task is to improve the bank's marketing efforts by predicting whether a customer will subscribe to a term deposit based on their characteristics and past interactions. This will allow the bank to:
* Increase efficiency: By targeting marketing calls more effectively, the bank's resources will be used more efficiently.
* Improve ROI (return on investment): With the same number of calls, the bank can generate more successful subscriptions.
* Enhance customer experience: Better targeting means calling customers who are interested, which can lead to increased customer satisfaction.

### The Data 
The data can be found at the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/222/bank+marketing). The marketing campaigns were based on phone calls and we will build a model that predict how likely clients will subscribe to a bank term deposit. More information on the original study can be found [here.](https://github.com/tildahh/MLBankMarketingAnalysis/blob/main/CRISP-DM-BANK.pdf)

### Findings
* KNN had the lowest performance among the models, indicating potential overfitting and lower precision.
* \[**Winner**\] SVM demonstrated the highest performance in terms of accuracy and precision but required significantly more computational time for training.
* Logistic Regression provided a good balance of performance and efficiency, demonstrating high accuracy and precision with a relatively quick training time.

### Next steps & recommendations
* Test using different numbers of features to see how it affects model performance.
* Continue tuning hyperparameters to optimize the models further.
* Test Random Forest or XGBoost models instead of Decision Tree since they are highly prone to overfitting and can potentially offer better performance.

For a detailed analysis, refer to the [Jupyter Notebook](https://github.com/piyalidas28/ML_AI_UCB/blob/main/practical_application_3/prompt_III.ipynb).
