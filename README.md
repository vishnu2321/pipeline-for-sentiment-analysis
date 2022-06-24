# Twitter-sentiment-analysis

Problem: Twitter is one of the biggest social media platform with millions of users. Hence, for better understanding the tweets and sentiment of users, sentiment analysis is used.

The data is taken from kaggle.
Dataset URL: <https://www.kaggle.com/datasets/kazanova/sentiment140>

The data is of format CSV.
The dataset is balanced dataset with 1.6 million tweet records with 5 attribute columns and a class column (i.e; sentiment of corresponding tweet).

### Columns in dataset

    - label (sentiment of tweet)
    - id
    - timestamp
    - query
    - username who tweeted
    - tweet

---------------------------------------------------------------------------------------------------------------------------------

### Data preprocessing

The data is loaded into spark dataframe and repartitioned into 4 partitions for parallel processing across multiple executors.
This model is focused on generalized sentiment of tweet and not for a specific user, hence username is dropped.
Id, timestamp, query does not effect the model and hence are dropped.

The data contains 0.8 million +ve tweets and 0.8 million -ve tweets.

---------------------------------------------------------------------------------------------------------------------------------

### Custom transformer for Pyspark ML pipeline

A pipeline contains a series of transformers and estimators which takes data ,transforms and process them.
The custom transformer inherits transformer class.
The custom transformer in this consists of several data transforming steps, as follows:

    - Converting tweet to lower case
    - Removing Stopwords
    - Cleaning Puntuations
    - Removing repeating characters
    - Cleaning URL's
    - Removing numerical's
    - Tokenizing
    - Stemming
    - Lemmatizing

---------------------------------------------------------------------------------------------------------------------------------

Adding transformer to pipeline stages.
HashingTF and IDF converts tweets to floats for computation of the model, and are added to the stages.
Fitting the data into the pipeline.
The dataset is split into training and testing using randomsplit.

---------------------------------------------------------------------------------------------------------------------------------

### Training and Testing the model

Logisitic regression with differernt parameters/attributes are used.
The accuracy of the model is 85.3%.

Training dataset area under ROC: 0.934
Testing dataset area under ROC: 0.738

---------------------------------------------------------------------------------------------------------------------------------

Time taken by pandas --- 177.6mins
Time taken by Pyspark APIs --- 109mins
