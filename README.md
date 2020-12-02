# Analysing 2 million Tweets using Python 

## Project Goals 
During my MSc, my thesis was focused on the broad goal of understanding why and how people choose to share information in a political context and how this is impacted by sentiment, whether a tweet is news and whether it endorses a campaign that the user supports. The investigative goals were as follows:
* To understand whether the sentiment of a tweet is correlated with the number of re-tweets and whether this is impacted by
    * A tweet being classified as 'news'  
    * The political affiliation of the tweet (i.e. whether users are more likely to re-tweet 
    
While this page contains a summarised version of my project, feel free to access the full thesis document [here](http://bit.ly/trisha_thesis) or alternatively watch this [video of a workshop I delivered remotely for the British Library] (http://bit.ly/britishlib_video) for students looking to conduct research projects using social media data 

## Project Tools 
To do this, I used a publicly available dataset containing Twitter data which you may download [here](https://catalog.docnow.io/) titled "Ireland 8th amendment referendum vote". Alternatively, the .txt file is also included in repository. I chose to use Python given its ease to work with and R/ R Studio's speed limitations in processing big data. Writing in Python 3.5, I used Jupyter Notebook and Anaconda employing the following packages during the analysis. Feel free to access the full script [here](https://github.com/trisharjani/twitter_sentment_python/blob/master/Cleaning_Sentiment_News.ipynb). 

* Numpy 
* Pandas 
* Seaborn

## Data Cleaning & Simple Classification 

*1. Removing all spam, non-english tweets* 

Spam tweets were determined by calculating the 'follower to friend' ratio based on the idea that users with a high ratio i.e. those who have more followers than they are following have been shown to have low reciprocity and are likely to be politicians or generally popular users. Conversely, those with a ratio lower than 0.01 were classified as spam implying that a user following 5000 individuals with only 50 followers would be classified as spam. Language was one of the variables provided by twitter thus this was a simple filtering mechanism 

*2. Assigning Tweet an Endorsement Score* 

This was done using hashtags. During data collection, hashtags were employed to select which tweets were relevant from twitter. Manual classification of these tags into supporting the 'yes', 'no' or 'neutral' outcome in the referendum. Examples of hashtags include #voteyes (yes endorsement) or #Togetherforno (no endorsement), #8thref, #hometovote (neutral but relevant). The full list of hashtags can be found on page 54 of the full document. 

Classification and basic tweet composiiton was as follows, 

| Endorsement       | Total Tweets | Total Retweets | 
| ----------------- | :----------: | :------------: | 
| Yes Campaign (2)  | 646,897      | 497,169        |
| No Campaign (3)   | 118,241      | 90,699         |
| Neither (1)       | 284,515      | 71,910         |
| Both/ Unclear (4) | 33,574       | 23,075         |          

*3. Assigning Tweets a Sentiment* 

In order to assign tweets a sentiment, each tweet was run through a sentiment analyser called VADER (Valance Aware Dictionary and Sentiment Reasoner). This is a rule-based model for sentiment analysis and was developed specifically for analysing sentiments on social media. It is fully open-sourced under the MIT license. Within python, VADER is a module in the so-called nltk or natural language toolkit, a platform built to work with human language data. VADER has shown to perform exceptionally on social media texts, which Hutto and Gilbert (2014) claim have 96% accuracy.

[Link to Vader GitHub Page](https://github.com/cjhutto/vaderSentiment)

*4. Filtering by Users of Importance* 



## Exploratory Data Analysis
Heatmap of correlations:

<img src="https://github.com/trisharjani/twitter_sentment_python/blob/master/images/heatmap_correlations.jpg" width="400" height="300"/>

## Sentiment Analysis
Average Sentiment of Tweets over Time: 
![alt text](https://github.com/trisharjani/python/blob/master/images/sentiment_over_time.jpg "Sentiment over Time")

## Network Analysis

<img src="https://github.com/trisharjani/python/blob/master/images/network%20mapping.jpg" width="600" height="700"/>

## Regression Analaysis 



## Summary of Conclusions 

### Bibliography #### 

Hutto, C. ., & Gilbert, E. (2014). VADER: A Parsimonious Rule-based Model for Sentiment Analysis of Social Media Text. Eighth International Conference on Weblogs and Social Media. Retrieved from http://comp.social.gatech.edu/papers/icwsm14.vader. hutto.pdf.

