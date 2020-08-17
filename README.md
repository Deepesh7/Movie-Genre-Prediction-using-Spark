## **Movie Genre Prediction with Spark**

**The task of this assignment is to use machine learning algorithms in apache spark to predict the movie genre. A data-item can be associated with multiple movie genres.**

### Step 0: **Initial steps to use spark in the Ubuntu Virtual Machine. (Optional)**

1.  Installing OpenJDK by executing the following command:
`sudo apt-get install openjdk-8-jdk`
2. Change the default version of java by executing the following command:
`sudo update-alternatives --config java`
3. Selecting mode 3 with path /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java.

### Part 1
#### Preprocessing
- We are loading the file, tokenizing into words, and converting to lower case using Regex Tokenizer.
- We are removing the stopwords from the text to input quality data into our model.
- The result of this step is stored in the ‘filtered’ column in our train data. This column contains an array of words.
- We are preprocessing the mapping.csv to append columns to the training data for each movie genre. Eg: ‘Drama’, ‘Comedy’. The respective movie genre column will contain 1 if the movie is of that genre and 0 otherwise.
- We are following the same preprocessing steps on test data to match the training data.

#### The method used in selecting features.
- We are using Count Vectorizer on the preprocessed data to convert words into a vector for use in the machine learning model.

#### Machine learning model used.
- We are using LogisticRegressionWithLBFGS to train the model and predict on the test data.
- We store the test data as a copy in test-result.
- For each value of a genre, we are running a loop where we train our input data using LogisticRegressionWithLBFGS.
- We first need to convert the ml.Vector to mllib.Vector. We do this by using MLUtils.
- We train our input data and have saved the trained ML models. We load this model to predict our test data. We only send movie_id and test ‘features’ to the predict method.
- The output consists of col names as ‘_1’ and ‘_2’. We rename this to ‘movie_id’, genre value respectively.
- We are appending a column to the test_result data which displays predicted results for each movie on that genre. (This is the output of for loop)
- Finally, we are combining all the genre prediction columns into ‘predictions’ column and writing as a CSV file.
- After uploading the CSV file on Kaggle, the resultant macro F1 Score: 0.97247

### Part 2
#### Preprocessing
- We are loading the file, tokenizing into words, and converting to lower case using Regex Tokenizer.
- We are removing the stopwords from the text to input quality data into our model.
- The result of this step is stored in the ‘filtered’ column in our train data. This column contains an array of words.
- We are preprocessing the mapping.csv to append columns to the training data for each movie genre. Eg: ‘Drama’, ‘Comedy’. The respective movie genre column will contain 1 if the movie is of that genre and 0 otherwise.
- We are following the same preprocessing steps on test data to match the training data.

#### The method used in selecting features.
- We are using hashingTF on the preprocessed data to convert tokenized words into the frequency of words based on hashed-indexes.
- We then transform our training and test data.
- We apply the output of transformation to the IDF model to create Inverse document frequency.
- We are passing the result of IDF on our machine learning model.

#### Machine learning model used.
- We are using LogisticRegressionWithLBFGS to train the model and predict on the test data.
- We store the test data as a copy in test-result.
- For each value of a genre, we are running a loop where we train our input data using LogisticRegressionWithLBFGS.
- We first need to convert the ml.Vector to mllib.Vector. We do this by using MLUtils.
- We train our input data and have saved the trained ML models. We load this model to predict our test data. We only send movie_id and test ‘features’ to the predict method.
- The output consists of col names as ‘_1’ and ‘_2’. We rename this to ‘movie_id’, genre value respectively.
- We are appending a column to the test_result data which displays predicted results for each movie on that genre.(This is the output of for loop)
- Finally, we are combining all the genre prediction columns into ‘predictions’ column and writing as a CSV file.
- After uploading the CSV file on Kaggle, the resultant macro F1 Score: 0.97658.

### Part 3
External Libraries:
Spark nlp
Pickle
Spark ml (nGram)
Spark mllib (MLUtils)

#### Preprocessing
- We are loading the file, tokenizing into words, and converting to lower case using Regex Tokenizer.
- We are removing the stopwords from the text to input quality data into our model.
- The result of this step is stored in the ‘filtered’ column in our train data. This column contains an array of words.
- We are preprocessing the mapping.csv to append columns to the training data for each movie genre. Eg: ‘Drama’, ‘Comedy’. The respective movie genre column will contain 1 if the movie is of that genre and 0 otherwise.
- We are following the same preprocessing steps on test data to match the training data.

#### The method used in selecting features.
- We tried to train our model using Word2Vec, LDA (Topic Modelling), WordEmbedding (Spark NLP), and nGram of size 2 and 3. We finally got the best result using nGram with size 2.
- We use nGram model to transform the input data into ngrams of size 2 which helps our model to understand the context better.
- We transform both our train and test using nGram.
- We are then using CountVectorizer on the output of our nGram with numFeatures as 10000.
- The output of the count vectorizer is given to the model for training.

#### Machine learning model used.
- We are using LogisticRegressionWithLBFGS to train the model and predict on the test data.
- We store the test data as a copy in test-result.
- For each value of a genre, we are running a loop where we train our input data using LogisticRegressionWithLBFGS.
- We first need to convert the ml.Vector to mllib.Vector. We do this by using MLUtils.
- We train our input data and have saved the trained ML models. We load this model to predict our test data. We only send movie_id and test ‘features’ to the predict method.
- The output consists of col names as ‘_1’ and ‘_2’. We rename this to ‘movie_id’, genre value respectively.
- We are appending a column to the test_result data which displays predicted results for each movie on that genre. (This is the output of for loop)
- Finally, we are combining all the genre prediction columns into ‘predictions’ column and writing as a CSV file.
- After uploading the CSV file on Kaggle, the resultant macro F1 Score is: 0.98650.

