# Stack-Overflow-Tag-Predictor

 ## Description
 
Stack Overflow is the largest, most trusted online community for developers to learn, share their programming knowledge, and build their careers.

Stack Overflow is something which every programmer use one way or another. Each month, over 50 million developers come to Stack Overflow to learn, 
share their knowledge, and build their careers. It features questions and answers on a wide range of topics in computer programming. 
The website serves as a platform for users to ask and answer questions, and, through membership and active participation, to vote questions and
answers up or down and edit questions and answers in a fashion similar to a wiki or Digg. 
As of April 2014 Stack Overflow has over 4,000,000 registered users, and it exceeded 10,000,000 questions in late August 2015. 
Based on the type of tags assigned to questions, the top eight most discussed topics on the site are: Java, JavaScript, C#, PHP, Android, jQuery, Python and HTML.

### Problem Statemtent

Suggest the tags based on the content that was there in the question posted on Stackoverflow.
Source: https://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction/

Source / useful links

1. Data Source : https://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction/data
2. Youtube : https://youtu.be/nNDqbUhtIRg
3. Research paper : https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/tagging-1.pdf
4. Research paper : https://dl.acm.org/citation.cfm?id=2660970&dl=ACM&coll=DL

## Real World / Business Objectives and Constraints

1. For the given Questions and its descriptions, Predict as many tags as possible with high precision and recall.
2. Incorrect tags could impact customer experience on StackOverflow.
3. No strict latency constraints.
4. If a incorrect tag is predicted, then the precision decreases and if any correct tag is missed then recall decreases.

## Data
### Data Overview

Refer: https://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction/data

All of the data is in 2 files: Train and Test.

1. Train.csv contains 4 columns: Id,Title,Body,Tags.
2. Test.csv contains the same columns but without the Tags, which you are to predict.
3. Size of Train.csv - 6.75GB
4. Size of Test.csv - 2GB
5. Number of rows in Train.csv = 6034195

The questions are randomized and contains a mix of verbose text sites as well as sites related to math and programming. The number of questions from each site may vary, and no filtering has been performed on the questions (such as closed questions).

### Data Field Explaination

Dataset contains 6,034,195 rows. The columns in the table are:

1. Id - Unique identifier for each question
2. Title - The question's title
3. Body - The body of the question
4. Tags - The tags associated with the question in a space-seperated format (all lowercase, should not contain tabs '\t' or ampersands '&')

## Mapping the real-world problem to a Machine Learning Problem
### Type of Machine Learning Problem
1. This Stack-overflow problem is multi-label classification problem, where each question have multiple labels/tags/classes.

#### Multi-label Classification: Multilabel classification assigns to each sample a set of target labels. 
This can be thought as predicting properties of a data-point that are not mutually exclusive, such as topics that are relevant for a document.
A question on Stackoverflow might be about any of C, Pointers, FileIO and/or memory-management at the same time or none of these.

2. In binary classification and multi-class classification we only have one label for each Xi. 
When we have multiple labels for a given Xi then it multi-label classification problem.

Credit: http://scikit-learn.org/stable/modules/multiclass.html

## Performance metric

### F1-score, Micro-averaged F1-score, Macro averaged F1-score

#### F1-score:- The F1 score can be interpreted as a weighted average of the precision and recall. 
To get both high precision and high recall, we can use F1-score which is a geometric mean of both precision and recall. 
where an F1 score reaches its best value at 1 and worst score at 0.

1. For F1-score minimum value is 0 and best value is 1.
2. The relative contribution of precision and recall to the F1 score are equal. The formula for the F1 score is:
3. F1 = 2 (precision * recall) / (precision + recall) . This is for binary classification.
4. Precision = True positives / True positives + False positives
5. Recall = True positives / True positives + False Negatives.

In multi-label classification we can modify F1-score into 2 types

a. Micro-averaged F1-score. It is more popular

b. Macro averaged F1-score

#### Micro-Averaged F1-Score (Mean F Score) :- This is the weighted average of the F1 score of each class.

1. Here weightage is given based on how frequently a label occurs.
2. It takes tag/label frequency of occurance into consideration when computing micro precision and micro recall.
3. Here we take individual TP, FP, FN, so we get weighted average of these and we get weighted F1-score.
4. Calculate metrics globally by counting the total true positives, false negatives and false positives.
5. This is a better metric when we have class imbalance.

#### Macro f1 score:-

1. Calculate metrics for each label, and find their unweighted mean. This does not take label imbalance into account.
2. It takes simple average of F1 scores of all labels/tags.
3. It doesn't take frequency of occurance of a tag into consideration. This is non-weighted, simple F1-score.

If we have a case where some tags occurs many times and some tags occurs very less times, then it is good to use micro averaged F1-score , not macro averaged F1-score.

#### Reference:-

https://www.kaggle.com/wiki/MeanFScore

http://scikit-learn.org/stable/modules/generated/sklearn.metrics.f1_score.html

Hamming loss : The Hamming loss is the fraction of labels that are incorrectly predicted. If the actual labels and predicted labels differ more, then the error also increases. This is Hamming loss.

https://www.kaggle.com/wiki/HammingLoss
