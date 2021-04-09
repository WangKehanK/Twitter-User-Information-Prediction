# CS505
## Main tasks

Main tasks can be devided into three part: Gender, age, and Race prediction. Details explained as following: 

### Gender
- [Gender](Twitter_User_Gender.ipynb)
- TODO: 
  - Predict gender for each user (we only did 1 user right now)
  - Calculate accuracy based on human.labeled.gender & lexicon.gender.prediction 


Using m3inference, you can predict gender.
```
 'output': {'age': {'19-29': 0.147,
                    '30-39': 0.8197,
                    '<=18': 0.0049,
                    '>=40': 0.0285},
            'gender': {'female': 0.0006, 'male': 0.9994},
            'org': {'is-org': 0.0, 'non-org': 1.0}}}
```
- Can we just say the above-given user is a male? 
Yes, you can

### Age
- [Age](Twitter_User_Age.ipynb)
- TODO: 
  - Scrap 100 tweets for each user
  - Build BERT
  - Predict Age
  - Calculate accruacy based on human labeled value

For age prediction (<21, >=21), you can use m3inference (but their prediction for age is not so great), so you should use Tweepy as before to get each user's last 100 tweets, convert them to vectors using BERT's last 4 layers (and concatenate, you can see: https://github.com/google-research/bert#using-bert-to-extract-fixed-feature-vectors-like-elmo for extracting vectors from the last 4 layers given a tweet), then use logistic regression or other machine learning model trained on the age annotation in the "human_labeled_age" column in the annotated data (changing this column first to <21 and >=21 age labels) to train age prediction based on user tweets. 

### Race
- [Race](Twitter_User_Race.ipynb)
- TODO:
  - Explore another method 
  - Calculate accuracy

Use https://github.com/appeler/ethnicolr for predicting race. 

## Response

When I was using M3 inference, it outputs a json for each user like this:

```
 'output': {'age': {'19-29': 0.147,
                    '30-39': 0.8197,
                    '<=18': 0.0049,
                    '>=40': 0.0285},
            'gender': {'female': 0.0006, 'male': 0.9994},
            'org': {'is-org': 0.0, 'non-org': 1.0}}}
```
1. How can I determine the exact age when the age was given a range? 

To determine the exact age, you cannot use m3 inference. You must build your own classifier that is based on user tweets that I mentioned before in my previous email. 

2. Can we just say the above-given user is a male? 

yes, you can

3. the human label value(age, gender, etc..) in the given dataset has a lot of NULL values, how can we compare two values?

for NULL values, you cannot evaluate. So for evaluation, use only non-null values in that file for labeled age (to evaluate your age prediction), and labeled_gender (to evaluate your gender prediction)



Under: 
https://github.com/euagendas/m3inference#existing-json-twitter-data

You can see that if you have crawled tweets from the user based on their IDs (using Twitter API with a library that we use in Assignment 2: one example of a library would be tweepy: https://fairyonice.github.io/extract-someones-tweet-using-tweepy.html), in this format: https://github.com/euagendas/m3inference/blob/master/test/twitter_cache/example_tweets.jsonl

Then from the tweets, you can use the tool to get the profile pictures of the users. 

Using m3inference, you can predict gender, then use https://github.com/appeler/ethnicolr for predicting race. 

For age prediction (<21, >=21), you can use m3inference (but their prediction for age is not so great), so you should use Tweepy as before to get each user's last 100 tweets, convert them to vectors using BERT's last 4 layers (and concatenate, you can see: https://github.com/google-research/bert#using-bert-to-extract-fixed-feature-vectors-like-elmo for extracting vectors from the last 4 layers given a tweet), then use logistic regression or other machine learning model trained on the age annotation in the "human_labeled_age" column in the annotated data (changing this column first to <21 and >=21 age labels) to train age prediction based on user tweets. 
