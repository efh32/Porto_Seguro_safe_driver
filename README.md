# Porto Project
1) Preprocess Data
Files - explore_data.py, preprocess_data.py

explore_data.py - Found in Model-2
  1) Reads the raw train data and raw test data.  (Files from the competition)
  2) Drops columns that have too many missing values.  
  3) Imputes missing values with sklearn.preprocessing Imputer.  Replaces missing categorical data with the column mode.  Replaces missing continous data with the column mean.
  4) I divided the columns by label.  I checked each column to see whether the distributions of the column are similar.  If the distributions of the columns are too similar, I remove the column.
  5) Checked the distributions of each column in test and train data.  If the test data and train data distribution differed, we remove the column.  The column would not train a good model if the test data and train data differed too much in distribution.  In this case, all were similar between the test data and train data.
  6) Writes out the preprocessed train and test data.
  
Links:
  1) Imputer example - https://machinelearningmastery.com/handle-missing-data-python/
  2) Visual example of choosing which columns to remove - https://github.com/Currie32/Predicting-Credit-Card-Fraud/blob/master/Predicting_Credit_Card_Fraud.ipynb
  

preprocess_data.py - Found in Model-2
  1) Reads the train data (From the competition). 
  2) Creates training data and testing data For the model.  The training data is 80% of the original train data.  The testing data is the remaining 20% of the original train data.
  3) Writes the training data and testing data to csv files.
  4) Creates an augmented training set.  We take 400,000 data points from training data that have a label of 0.  We use resample from sklearn to increase the number of data that is labeled 1.  What we increase the number of times each data point that has a label of 1 shows up until it is balanced with the data that has a label of 0.  This is how we deal with class imbalance.
  5) Write out the autmented training data.

It is important to note that we are training the wide and deep model with the augmented training set.  The original training set we created still has a use to us.  We can use it as kind of a testing set for our model.  We have to make sure the increase in the data with a label of 1 does not overfitt the data.  

Links:
  1)How to use resample to increase or decrease label - https://elitedatascience.com/imbalanced-classes
------------------------------------------------------------------------------------------------------------------------------------
2) Wide and deep model - train_wide_and_deep.py, w_n_d_predict.py

Trains a wide and deep model with the Augmented Data.  

Links:
1) Explains the Wide and Deep - https://www.tensorflow.org/tutorials/wide_and_deep
2) Video from the creator of Wide and Deep - https://www.youtube.com/watch?v=NV1tkZ9Lq48

-------------------------------------------------------------------------------------------------------------------------------------
Concepts:

Example of dealing with imbalanced Data using Softmax

1) Link for example: https://github.com/efh32/Credit-Card-Fraud-Detection/blob/master/model.py 

The following is code for this kaggle competition.
https://www.kaggle.com/dalpozz/creditcardfraud

The data is credit card information reduced and anonymized using PCA.  The goal of the competition is to tell whether credit card information is fraudulent or not.  The labels are also unbalanced for this data set.  

I used tensorflow neural networks to train the model.  

The following links may help explain what I did:

---------------------------------------------------------------------------------------------------------------------------------
Neural Networks

2) This link contains Andrew Ng's lecture about neural networks:
https://www.youtube.com/watch?v=1ZhtwInuOD0&list=PLLssT5z_DsK-h9vYZkQkYNWcItqhlRJLN&index=43

3) This link is a neural network playground to help understand neural networks:
http://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=4,2&seed=0.08509&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false

----------------------------------------------------------------------------------------------------------------------------------
Softmax 

Softmax is just multi-class logistic regression.

4) This is a link discussing softmax regression.
https://www.kdnuggets.com/2016/07/softmax-regression-related-logistic-regression.html

5) This link shows an applied use of softmax
https://www.tensorflow.org/get_started/mnist/beginners

----------------------------------------------------------------------------------------------------------------------------------
6) Link for Dealing with unbalanced data: 
https://blog.fineighbor.com/tensorflow-dealing-with-imbalanced-data-eb0108b10701

The key to dealing with unbalanced data is using softmax because we need the data points with no claim (target = 0) to have less weight on backpropagation (gradient descent) thant the data points with claim (targets)

------------------------------------------------------------------------------------------------
7) Wide and deep:
Possible solution to deal with sparse columns

https://www.tensorflow.org/tutorials/wide_and_deep