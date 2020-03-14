# Executive Summary

Many social networks receive tons of complaints and general comments on their services. The problem is that many of these comments and complaints are insincere or jokes. Insincere feedback is generally not useful, so it would be good to filter out insincere feedback.
  
We can use machine learning to predict whether or not a complaint is sincere or not. The data we are learning from is from the first world and fifth world problems subreddits. These subreddits contain examples of real complaints and fake complaints respectively. They also sit on the border between minor sincere complaints and insincere complaints, as these are the hardest to tell the difference between.
  
Our model is capable of classify questions with 89% accuracy. Our model is easy to implement, runs quickly, and will result in a reduced workload for community managers.
  
# How do we determine if posts are from  r/fifthworldproblems or r/firstworldproblems?
## Data Collection
Post data was collected using the Pushshift api. 20,415 posts with a minimum score of 1000 were collected from the subreddits. Data was stored in the results_dirty.csv
## Data Cleaning and EDA
Posts with missing, removed, or deleted selftext were dropped from the dataset. The resulting dataset was unbalanced in favor of r/fifthworldproblems, so posts from r.fifthworldproblems were deleted to balance the classes. It was found that there were no duplicate posts. The selftext and titles were combined into an alltext column for modeling purposes. The alltext column was tokenized and lemmatized to aid in nlp and for visualization. The following visualizations were created.
  
# Histogram
![hist](https://raw.git.generalassemb.ly/ZacharyJamesHill/dsi_assignments/master/project_3/visualizations/word_hist.png?token=AABiDjPuQkljUvd06TnteqDphmLyFrW6ks5eOvwOwA%3D%3D)
  
# TSNE Visualization
![tsne](https://raw.git.generalassemb.ly/ZacharyJamesHill/dsi_assignments/master/project_3/visualizations/tsne_scatter.png?token=AABiDuAYd2jvLKfYNJ5TeKYZpFhjKTX7ks5ePPABwA%3D%3D)

Finally the alltext column was detokenized and the data was output as results.csv
## Modeling
In order to classify posts the text of each post has to be tokenized and vectorized(encoding words in a sparse format similar to dummying). This was handled with sklearn's countvectorizer and tfidfvectorizer. Countvectorizer provides a sparse matrix of 1s and 0s, while tfidfvectorizer provides a sparse matrix of floats >= 1.  

The data was split into a train and a test for evaluation purposes.  

Grid search was used in order to find the best parameters for the vectorizer and model in each modeling attempt.  

The following models were used.
1. Bagging(of multiple models not just decision tree)
2. Decision Forest
3. Gradient Boosting
4. K Nearest Neighbors
5. Logistic Regression
6. Gaussian Bayes
7. Multinomial Bayes
8. Random Forrest
9. Support Vector Classifier

Logistic Regression provided the best accuracy with a 99% on train and a 89% on train.
  
## Conclusions
Determining between r/fifthworldproblems and r/firstworldproblems with reasonable accuracy is possible. Possible applications of this model include, automatic complaint filtering, generalized detection of absurd content, and novelty text classification. 