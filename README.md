Topic classification: an automated method to classify noun-phrases based on their topics

1. Description of raw dataset
The dataset of this project is acquired from Yahoo! Webscope in the category of language data and is named as “L19 - Yahoo! Answers browsing behavior, version 1.0”. The dataset has the size of 166 Gb, consisting of two folders, each having 100 files compressed in gzip form. Each file in the folders holds data in csv format with each field being delimited with tab (“\t”) characters.
The dataset was generated by Yahoo! News between January 2007 and July 2010. Noun-phrases which appeared at least 100 times and their context were extracted from news articles. There are eight (8) fields in the dataset, the description of each of which is as follows.
    • type: Original article type
    • np1, np2: Noun-phrases extracted from the article. If only one noun-phrase exists in the sentence, np2 is full
    • context: The context in which the noun phrases appeared
    • source: News channel from which the data is extracted
    • category: News items categories
    • location: Geographic location of the news channel
    • time: Day of publication, where day 0 is 1/1/1970
 
2. Target problem 
By adopting the chosen dataset, this project tends to tackle the problems in natural language processing in general and topic classification in particular.
Topic classification refers to the tagging of unseen sets of texts to known possible topics. It lies in the range of supervised machine learning where the algorithms are trained with text data that has been categorized with their labels, based on which the algorithms learn how to assign the most relevant topics to the unseen texts eventually.
For the aim this project, we will create the labels for the noun-phrase based on the source where it comes from. There are explicitly five labels including business, finance, health, politics, and sports. We then construct a Long Short-term Memory (LSTM) neural network and feed it with the noun-phrases and their labels. The model will be later used to tag equivalent topics to unseen noun-phrases.

3. Model formulation
We utilize a LSTM recurrent neural model in the light that the model will treat a set of sub-sentences based on their actual meaning and classify such texts into relevant topics. This is different from other non neural algorithms such as Naive Bayes or Support Vector Machine, where the set of strings is treated separately as word having no meaning, therefore, the output of the prediction results into every single word being classified into one of the categories. This is due to lack of the short-term memory and the vanishing gradient problem. 
We formulate two models, one without the weight regularization for over-fitting problem, and one with the weight regularization. The two models illustrate how the results improve and the over-fitting issues reduce after adding the factor of weight control.
The first layer of the model is an Embedding layer with three main parameters; the size of vocabulary, the number of dense embedding dimension, and the maximum length of tokenized texts. Next, we add into the model two layers of LSTM with 64 neurons for the first layer and 32 neurons for the second layers. In the first layer of LSTM, we set the argument “return_sequences” to be “True” to allow the output of the first layer to become the input of the second layer. We, then, place two dense layers into the model. The first dense layer contains 64 neurons and the output dense layer has 6 cells representing different categories. The reason for putting 6 cells into the output layer rather than 5 cells equivalent to 5 labels defined in the processing data part is that we denote the class label of the topics as 1, 2, 3, 4, and 5. Thus, setting 6 cells in the last dense layer will allow the model to understand to include the class 5 into training. 
In the model with the weight regularization, we add weight control in the form of sum of squared weights (L2). Due to time constraint, we did not resort to grid-searching to find the optimal value for the regularization but adopted a naive approach instead to come with the value of 0.001. We also have another layer of “Dropout” to alleviate the over-fitting problems. 

4. Data analysis
We can notice the improvement with the model contains dropout and learning rate to prevent overfitting.
To summarize, we successfully create a base model to implement recurrent neural network to train dataset from Yahoo! Webscope. We had the opportunities to explore the dataset, implement ETL and deep learning applications in Puhti. The performance can be improved by adding more layers while training or using different optimization methods.