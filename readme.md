# Instructions
Download the notebook and run it in colab.

Natural Language Processing - Sentiment Analysis
Team: Xian Han Chen (CIS 4190), Anson Yan (CIS 5190), Shi Yang Zheng (CIS4190) 
Project Mentor TA: Brian
Github Repository: https://github.com/AaruuC/SentimentAnalysis
## Abstract
For this project, we aimed to explore the potential of natural language processing (NLP) techniques in performing sentiment analysis. Specifically, we utilized a pre-trained language model and fine-tuned it on a labeled dataset of product reviews to predict sentiment. We chose to train our data on food reviews and we used a set of clothing reviews for our shifted dataset for additional model testing. We evaluated the performance of our model using various metrics, including accuracy, precision, recall, and F1-score, but we focused on F1-score since our labels were very imbalanced. Our results showed that all of the fine-tuned language models achieved high accuracy in predicting sentiment on the training and testing data sets, outperforming traditional machine learning models. However, only the BERT and RNN models performed well on the shifted data set, which led us to conclude that LSTM was poor at generalizing.
## Introduction
Set up the problem: The dataset we will be training and testing our model on will be the Amazon Fine Food Reviews dataset. We will use the review text and review score to train our model to predict whether a given piece of text has a positive, negative, or neutral sentiment. The inputs of our eventual machine learning model will be some sort of text data, such as reviews, comments, and tweets, and the output would be a sentiment score, where the value 1 indicates a positive sentiment, -1 indicates a negative sentiment, and 0 indicates a neutral sentiment.

Implementation contributions: We plan to use natural language processing that we will learn in class to implement sentiment analysis to predict the Amazon review star rating that accompanies the review. We’re considering several architectures for NLP such as RNN and LSTM.
Evaluation contributions: One method of determining model effectiveness is by converting the sentiment score into a rating and checking that it is similar to/matches the user’s rating. Another method of determining model proficiency will be to aggregate the results of our model and compare them against the average star rating of the products. For each architecture, we will analyze how well the model can determine positive or negative text depending on hyperparameters in our processes. 
2) How We Have Addressed Feedback From the Proposal Evaluations
Our project mentor suggested thinking about which evaluation method we plan to use, and we concluded that the best method would be the F1-score since our dataset consists mostly of positive reviews, and F1-score is a better evaluation method when the dataset is not balanced. We also plan to test our model on a dataset consisting of reviews of women’s clothing to ensure that our model is able to make accurate predictions on a variety of products. He also suggested looking for papers that work with sentiment analysis using various architectures for inspiration since our focus is to compare the efficacy of different architectures. 
## Background
1. LSTM on Amazon Fine Food Reviews
https://www.kaggle.com/code/rushabhwadkar/lstm-on-amazon-fine-food-reviews
The objective of this work is to determine whether a review is positive or negative using the
LSTM architecture which we are interested in comparing between other architectures. The
example code will be very helpful to build upon for our implemented LSTM.
2. Text classification using BERT
https://www.kaggle.com/code/nayansakhiya/text-classification-using-bert
BERT, a bidirectional transformer, was used to classify covid text data, as extremely negative,
negative, neutral, positive, and extremely positive. We edited BERT to only use two labels, classifying sentiment scores greater than or equal to 3 as positive and sentiment scores less than 3 as negative. The accuracy of this model was very good and we can compare BERT architecture with other neural networks or transformers.
## Summary of Our Contributions
Implementation contribution(s):
We implemented a variety of different neural network architectures, such as RNN, BERT, and 
Bidirectional LSTM. We tried varying the hyperparameters of each neural network architecture to analyze and find the best approach for our datasets. We also performed a dataset shift by training our models on food reviews and testing them on clothing reviews.
Evaluation contributions:
We determined our model effectiveness by converting the sentiment score into a rating and checking that our model is able to predict the correct sentiment (-1, 0, or 1). For each architecture, we tested different hyperparameters in our models, and kept the best performing hyperparameters in our final model.
## Detailed Description of Contributions
5.1 Implementation Contributions
For our baseline approach, we performed the logistic regression for sentiment analysis of food reviews. We set the model such that it would constantly predict a rating of 5. We chose to implement and systematically compare a wide variety of different approaches rather than implementing a novel algorithm to extend our cited works. During the implementation of the Bidirectional LSTM model for sentiment analysis of food reviews, several key contributions were made to ensure a robust and effective model. Firstly, the text data was preprocessed by tokenizing and padding the sequences to a fixed length, ensuring that the input data was consistent in shape and size. Then, we map the score of 1 or 2 to -1, 3 to 0, and 4 or 5 to 1. Additionally, a custom metric was implemented to evaluate the model's F1 score, a commonly used metric in sentiment analysis tasks and in evaluating imbalanced datasets. To improve the model's performance, hyperparameters such as the learning rate and batch size were tuned, and early stopping was used to prevent overfitting. Finally, to further optimize the model, transfer learning techniques such as fine-tuning were employed, which involved retraining the model with reduced learning rates and increased epochs. Afterward, a dataset shift was performed to evaluate the performance of the model. The model is trained using the food reviews dataset and tested using the clothing reviews dataset. Similarly, we created a RNN model and performed the same processes on the RNN model. We also trained the data set on a pre-trained BERT model with fixed model layer hyperparameters to create a baseline for a well-trained model.
5.2 Evaluation Contribution
Our models were designed to predict sentiment score (positive, negative, neutral). We predicted that the BERT model would have the best performance on generalizing to other datasets. Our first baseline model was the initial simple logistic regression model that we trained on the Amazon Fine Foods dataset which resulted in an overall accuracy of 0.603. However, we realized that the dataset classes were very imbalanced with a vast majority of the review ratings at 5. To account for this, we decided to use f1 score as a metric since it would better show the robustness of our models. The f1 scores for the logistic regression model were [0.244, 0, 0.188, 0.147, 0.772] for each of the review ratings. It performed much better on reviews with a rating of 5 even accounting for the imbalanced classes, but it was clear that logistic regression would not be ideal for our intended task since a dummy model that predicted that all reviews had a rating of 5 did not have marginally worse f1 scores [0, 0, 0, 0, 0.785]. We used a set of clothes reviews as a shifted dataset. The logistic regression model performed similarly on this shifted dataset with f1 scores of [0.147, 0.060, 0.161, 0.244, 0.719] and the dummy model performed as expected with  [0, 0, 0, 0, 0.713]. Our first more specialized model was the pretrained BERT model at the suggestion of our project mentor TA. It performed exceptionally well with a test F1 score of 0.923 after only 3 epochs. Surprisingly, when the random state seed was not set, it sometimes performed even better when testing on the shifted dataset with an F1 score of 0.945. This could happen because of multiple reasons, including more difficult wording in the food reviews or noise in either datasets, but the fact that we trained on a pretrained model of BERT specialized for sequence classification was probably the biggest factor, since it is very likely that the language for clothes reviews is more general than food reviews. We also created and tested an RNN model that was able to achieve an f1-score of about 0.9, which is relatively successful when compared to the pre-trained BERT model. It was also able to perform relatively well on the clothing reviews dataset, achieving an f1-score of about 0.76, indicating that it is capable of generalizing to different situations. For the last model, bidirectional LSTM, it performed poorly with f1-score around 0.1. However with the added features of early stopping and optimizer, it performed exceptionally well and after further tuning of hyperparameters of the models, it achieved a f1-score of 0.9983. But the bidirectional LSTM did not perform as expected when tested with the shifted model and did much worse compared to the BERT and RNN models.
## Compute/Other Resources Used
Since the f1-score metric was removed from keras, we found a method of calculating the f1-score on StackExchange. (https://datascience.stackexchange.com/questions/45165/how-to-get-accuracy-f1-precision-and-recall-for-a-keras-model)
## Conclusions
We were able to develop various models and achieve high f1-scores for them, indicating that they are able to successfully predict the sentiment of different bodies of text. We learned the importance of tokenizing the inputs, as it makes it easier for our models to learn and process the data. We also learned that hyperparameter tuning was important for achieving a high f1-score for our models, as the f1-scores we had initially computed were around 0.7. The models we used could potentially be used to predict the sentiment in other texts, as we have shown that our model, despite being trained only on Amazon Fine Food Reviews, was successful in predicting the sentiment of clothing reviews.
We were unable to aggregate the results of our model and compare them against the average star rating of the products due to time constraints and having difficulties deciding on how to interpret our results. Our project mentor helped steer us in the right direction, as he suggested that we convert the ratings into a sentiment score and to consider the different evaluation metrics we would want to use. We also followed his suggestion to use the pre-trained BERT model to have some results to compare to and try to achieve.
In conducting sentiment analysis using natural language processing (NLP), there are several ethical considerations that must be taken into account. Specifically, when training on review datasets for the purpose of improved customer experience as well as increased transparency and accountability from product creators, we must ensure that other factors besides the review text should be considered to avoid review manipulation (either positive or negative).  
Expanding NLP sentiment analysis from reviews to more general applications creates many more challenges. General NLP models must be trained on diverse and representative datasets to avoid perpetuating biases and stereotypes. Additionally, it is important to ensure that the use of sentiment analysis does not violate individuals' privacy or infringe on their freedom of expression. Another ethical concern is the potential for NLP-based sentiment analysis to be used for manipulative purposes, such as targeted advertising or political campaigning.
