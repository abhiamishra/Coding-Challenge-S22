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

## Attempt One

The very first attempt was an attempt that utilized a simple random forest classification. The reason I used a random forest classifier as my primary method was due to a various number of reasons. The first reason was that in random forest classification, the number of decision trees all coming and using different features in random variations gives us a good way to control the amount of **bias in our final answer**. Since we have random decision trees all working in an ensemble, our final answer/classification has less bias and as such, gives us a more accurate classification. In addition, in data where there is colinearity - features relate to each other - random forest classification has been proven to be effective. In our dataset, we have data about various parts of a mushroom and inadverdently there will be some relation with a mushroom's properties to each other. As such, I went with random forest classification as my classfier.

  # Preprocessing
   
  I started my preprocessing with splitting my dataset in a 75/25 split to training dataset and testing dataset. After splitting my dataset, I encoded my features as all the   features provided are categorical variables and there needed to be a way to represent in them numerical format. As such, I utilized one-hot encoding, a common technique, on   my features and label encoding, which gave 0 to the edible class and 1 to the poisonous class, to my classifying variable. After encoding my features, and since they were     already 0s and 1s, there was no need for feature scaling.
  
  # Model Creation and Testing
  Used random forest classifier with 100 decision trees and tested on the testing dataset with an accuracy of **100 %** and a F-1 score of **100 %**. Accuracy, self-explanatory, measures our percent statistic of getting our predictions correct. F-1 Score on the other hand calculates the **harmonic mean between precision and recall**. Precision is defined as how many true positives out of all the predicted positives - allowing us to measure how accurate we were in predicting positives. Recall is defined as how many predictions that we get right from all the true positives - allowing us to measure the volume in predicting positives. There is an inherent tradeoff between tehse two metrics and as such, F-1 score attempts to provide a balanced view of what both metrics measure. A F-1 score indicates a balanced metirc of performnace of a model. In the classification matrix, there were no false positives or false negatives. As such, this model was succesful!
  
  # Caveats
  There is a sly problem here. The number of features accompanied with the high accuracy score and metrics means that this model may be overfitted to the sample data provided. In the real world settings, with the variability in data, this model may being to perform poorly. In addition, the number of features required in this model not only mean it may not be feasible for real-world scenarios but also the fact that the model might be overfitted and using features that are not really necessary for the classificatio.

# Attempt Two
