# Project 3: Web Scraping and NLP

## Author: Mario Sanchez, Jr.
## Date: 7/12/19


# Question:

Can text from Reddit be used to guess which show a user is talking about?

# Objectives:

- Obtain text data from reddit posts
- Decide on a model that classifies best
- Which words mattered most?
- How can we use this information to improve our marketing?


# Data Description:

- Two subreddits were picked, breakingbad and bettercallsaul.
- 815 unique posts obtained from breakingbad subreddit
- 771 unique posts obtained from bettercallsaul subreddit


# Data Dictionary:

| Column       | Description                                |
|--------------|--------------------------------------------|
| author       | person who wrote post                      |
| created_utc  | date posted                                |
| downs        | number of down votes                       |
| num_comments | number of comments on post                 |
| score        | score assigned by reddit                   |
| selftext     | text found within post                     |
| title        | text in the title of post                  |
| ups          | number of up votes                         |
| subreddit    | target (1: breakingbad, 0: bettercallsaul) |
| all_text     | combination of title and self text columns |
| word_count   | number of word contained within post       |


## Sources: 
1. https://www.reddit.com/r/breakingbad/
2. https://www.reddit.com/r/betterCallSaul/
3. https://www.imdb.com/title/tt0903747/
4. https://www.imdb.com/title/tt3032476/?ref_=nv_sr_1?ref_=nv_sr_1


## Target: NLP using classification models

# EDA and Model Selection:

1. Created scraper to obtain data from selected subreddits. Used over several days.

2. Each day was stored as a json and csv file to preserve all data.

3. Combined all days into a single dataframe for each subreddit. 

4. Assigned target value of 1 or 0 to each dataframe

5. Combine both subreddit dataframes in a single final dataframe

6. Feature Engineering:

- Combined "title' and "selftext" columns into a new "all_text" column to ensure every post contained text.
- Created a "word_count" column to display number of words per post.
- From "all_text"
    a. Removed punctuation
    b. Removed unusual characters such as "\n".
    c. Make sure other possible pieces of information are obtained from each post such as number of comments and date posted.

4. Model Preperation:

- tokenized words
    a. CountVectorize
    b. TfidfVectorizer
- lemmetized words
- count word frequency
- ensure there is not a large discrepancy between the number of target values

6. Models:

- Logistic regression
- K-nearest neighbors
- Multinomial Naive Bayes

# Model Performance:

After many different iterations, the following models were testest with above features to determine which performed best using the accuaracy score and observing the confusion matrix.

Additionally, plots of the word counts as well as their coefficients were plotted to visualize these numbers.

| Model                   | cvec | tfdf | lemm | Accuracy | True Positives |
|-------------------------|------|------|------|----------|----------------|
| Logistic Regression     | Y    | N    | N    | 77%      | 215            |
|                         | N    | Y    | N    | 78%      | 208            |
|                         | Y    | N    | Y    | 77%      | 212            |
|                         | N    | Y    | Y    | 77%      | 212            |
| KNN                     | Y    | N    | N    | 71%      | 212            |
|                         | N    | Y    | N    | 73%      | 207            |
| Multinomial Naive Bayes | Y    | N    | N    | 74%      | 184            |
|                         | N    | Y    | N    | 79%      | 202            |


Final Model Scores:

|  Final Model        | cvec | tfdf | lemm | Accuracy | True Positives | True Negatives | False Positives | False Negatives |
|---------------------|------|------|------|----------|----------------|----------------|-----------------|-----------------|
| Logistic Regression | Y    | N    | N    | 77%      | 215            | 150            | 30              | 81              |


# Primary findings/conclusions/recommendations:

- Using a logistic regression model we were able to predict which post the text was from 77% of the time. 
- Compared to other models that were tested, logistic regression was determined to be most accurate and interpretable.
- While this is not perfect, I believe that it can effectively be used to classify if a person is talking about Breaking Bad or Better Call Saul using only text.
- This model can then be used on other reddit, twitter, tvguide, etc. posts to determine if  people are talking about a certain show.
- This information can then be leveraged to direct your marketing efforts for new shows or projects related to these two great shows.


# Limitations and Assumptions:

- More data can improve models
- Using frequency of words is best for prediction
- Words included in the models did not just contribute noise to our model.


# Future Analysis:

- Utilize different text manipulation
- Test models on other TV show subreddits that lie in the say category
 


