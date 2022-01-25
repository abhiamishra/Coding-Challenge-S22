# ACM Research Coding Challenge (Spring 2022)

## [](https://github.com/ACM-Research/-DRAFT-Coding-Challenge-S22#no-collaboration-policy)No Collaboration Policy

**You may not collaborate with anyone on this challenge.**  You  _are_  allowed to use Internet documentation. If you  _do_  use existing code (either from Github, Stack Overflow, or other sources),  **please cite your sources in the README**.

## [](https://github.com/ACM-Research/-DRAFT-Coding-Challenge-S22#submission-procedure)Submission Procedure

Please follow the below instructions on how to submit your answers.

1.  Create a  **public**  fork of this repo and name it  `ACM-Research-Coding-Challenge-S22`. To fork this repo, click the button on the top right and click the "Fork" button.

2.  Clone the fork of the repo to your computer using  `git clone [the URL of your clone]`. You may need to install Git for this (Google it).

3.  Complete the Challenge based on the instructions below.

4.  Submit your solution by filling out this [form](https://acmutd.typeform.com/to/uTpjeA8G).

## Assessment Criteria 

Submissions will be evaluated holistically and based on a combination of effort, validity of approach, analysis, adherence to the prompt, use of outside resources (encouraged), promptness of your submission, and other factors. Your approach and explanation (detailed below) is the most weighted criteria, and partial solutions are accepted. 

## [](https://github.com/ACM-Research/-DRAFT-Coding-Challenge-S22#question-one)Question One

[Binary classification](https://en.wikipedia.org/wiki/Binary_classification) is a type of classification task that labels elements of a set (i.e. dataset) into two different groups. An example of this type of classification would be identifying if people had a specific disease or not based on certain health characteristics. The dataset found in `mushrooms.csv` holds data (22 different characteristics, specifically) about different types of mushrooms, including a mushroom's cap shape, cap surface texture, cap color, bruising, odor, and more. Remember to split the data into test and training sets (you can choose your own percent split). Information about the meaning of the letters under each column can be found within the file `attributelegend.txt`.

**With the file `mushrooms.csv`, use an algorithm of your choice to classify whether a mushroom is poisonous or edible.**

**You may use any programming language you feel most comfortable. We recommend Python because it is the easiest to implement. You're allowed to use any library or API you want to implement this, just document which ones you used in this README file.** Try to complete this as soon as possible.

Regardless if you can or cannot answer the question, provide a short explanation of how you got your solution or how you think it can be solved in your README.md file. However, we highly recommend giving the challenge a try, you just might learn something new!


## Explanation of My Answer

Binary classification is the task of classifying characteristics of a species between 0 (edible) and 1(poisonous). I had two attempts at trying to achieve this binary classification between an edible and poisonous mushroom. 

 Internet Documentation Used:
  - [sklearn package](https://scikit-learn.org/stable/modules/classes.html#module-sklearn.base)
  - [XGBOOST library](https://xgboost.readthedocs.io/en/stable/)
  - [Pandas](https://pandas.pydata.org/)
  - [NumPy](https://numpy.org/)
  - [Matplotlib](https://matplotlib.org/)
  - [Seaborn](https://seaborn.pydata.org/)

## Attempt One

The very first attempt was to utilize a **simple random forest classification**. I had multiple reasons to use a random forest classifier as my primary method. The first reason was that in random forest classification, the number of uncorrelated, decision trees all coming and using different features in random variations gives us a good way to control the amount of **bias in our final answer**. Since we have random decision trees all working in an **ensemble**, our final answer/classification has less bias and as such, gives us a more accurate classification. In addition, in data where there is **(multi) colinearity** - features relate to each other - random forest classification has been proven to be effective due to the ensemble process. In our dataset, we have data about various parts of a mushroom and inadverdently there will be some relation with a mushroom's properties to each other. To ensure that this does not affect my final result, I went with the random forest classification as my classfier.

  ### Preprocessing ###
   
  I started my preprocessing with an exploratory data analysis by looking at the distribution of the classes. The distribution was balanced and as such, there was no need to balance the data. I next proceeded to split my dataset in a **75/25 split to training dataset and testing dataset**. After splitting my dataset, I encoded my features as all the   features provided are categorical variables and there needed to be a way to represent in them in a numerical format. As such, I utilized **one-hot encoding**, a common technique, on my features and **label encoding**, which gave 0 to the edible class and 1 to the poisonous class, to my classifying variable. Note: There was no need for **feature scaling** since our features had been converted into 0s and 1s (the result of one-hot encoding).
  
  ### Model Creation and Testing ###
  Used random forest classifier with **100 estimators (decision trees)** and tested on the testing dataset with **an accuracy of 100 %** and **a F-1 score of 100 %**. 
  Accuracy, self-explanatory, measures our percent statistic of getting our predictions correct. F-1 Score on the other hand calculates the **harmonic mean between precision and recall**. **Precision** is defined as how many true positives out of all the predicted positives - allowing us to measure how accurate we were in predicting positives. **Recall** is defined as how many predictions that we get right from all the true positives - allowing us to measure the volume in predicting positives. 
  There is an inherent tradeoff between tehse two metrics and as such, F-1 score attempts to provide a balanced view of what both metrics measure. A F-1 score indicates a balanced metirc of performnace of a model. In the classification matrix, there were **no false positives or false negatives**. As such, this model was succesful!
  
  ### Caveats ###
  There is a sly problem here. The number of features accompanied with the high accuracy score and metrics means that this model may be **overfitted** to the sample data provided. In the real world settings, with the variability in data, this model may being to perform poorly. In addition, the number of features required in this model not only mean it may not be feasible for real-world scenarios but also the fact that the model might be overfitted and using features that are not really necessary for the classification.

## Attempt Two
In the second attempt, I tried to achieve the same results, this time doing it in a real-world setting. I attempted to use the same random forest classification with **feature selection and gradient boosting**. This tried to solve some of the caveats in attempt one while presenting a model that would be more useful in the real-world setting.

  ### Preprocessing ###
   The first task was to select our features. As said in attempt one, not all features are probably required to make the predictions and as such, I went about seeing which features have the strongest selection to the classifying variable.
   First, I encoded the feature variables with **ordinal encoding** - simply giving them a numerical encoding rather than a sequence of binary numbers - as to attempt feature selection. After that, I use the **Chi-Squared Statistic for independence** to find out which features are independent to the classifying variable. Features that have high scores correspond to lower independence while features with lower scores correspond to the higher independence. After calculating the Chi-Squared statistic for all the features, I graphed the score against the features to find which features were most useful. I found there were 6 features that had high relation to the variable and as such, I selected only those.
   
  ### Model Creation and Testing ###
  Since we were using only 6 features and we still wanted our model to be good, I opted to boost my random forest regression. **Boosting**, in simpler terms, takes a weaker model and makes it stronger by training its weaknesses. Combining boosting with an ensemble model can yield a stronger and more resilient model as not only do we have multiple decision trees arriving to random classifications but we also have a boosting which improves the weaker trees therefore yielding a stronger random forest. 
  For this booting algorithm, I chose **XGBOOST**, which stands for eXtreme Gradient Boosting, is a very strong version of normal gradient boosting. XGBOOST achieves high model performance at razor-sharp speeds which makes it a contender for choosing it for the boosting but there are other boosting models like AdaBoost and Simple Gradient Boosting. 
  In the end, XGBOOST was chosen because a) speed and performance, b) it builds upon gradient boosting which by itself attempts to boost models by looking at the difference between predictions and the true values which is an intuitive approach, and c) it is widely used by the industry.
  
  An XGBOOST random forest classifer was picked with **100 estimators (random trees)**, a subsample of 0.9 (an attempt for the model to create its own training/testing split within the training data provided), and a colsample_bynode of 0.7 (picking 70% of the features with different iterations of the trees). Finally, using cross-validation and the training dataset, the accuracy of the model came out to be 96.9%.
  
  When testing on the real testing dataset, the model gave **an accuracy of 96.8% and 65 false positives**. Looking at the classification report gave the **F-1 score at 97%** while there was a **94% precision rate for edible class** and **93% recall rate for poisonous class**. Overall, with less features selected, the model still gave a strong 97% accuracy score which is a success! We achieved a similar accuracy score as before with using less features and as such, preventing overfitting and allowing more translation into the real world!
  
   ### Caveats ###
   Caveats here include that there are other tests for doing feature selection and as such, while we picked some relevant features - we can do other testing like heatmaps and mutual information feature selection that can give us a better look what to pick to classify our mushrooms.
