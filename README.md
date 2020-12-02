# Analysing 2 million Tweets using Python 

## Project Goals 
During my MSc, my thesis was focused on the broad goal of understanding why and how people choose to share information in a political context and how this is impacted by sentiment, whether a tweet is news and whether it endorses a campaign that the user supports. The investigative goals were as follows:
* To understand whether the sentiment of a tweet is correlated with the number of re-tweets and whether this is impacted by
    * A tweet being classified as 'news'  
    * The political affiliation of the tweet (i.e. whether users are more likely to re-tweet)
    
While this page contains a summarised version of my project, feel free to access the full thesis document [here](http://bit.ly/trisha_thesis) or alternatively watch this [video of a workshop I delivered remotely for the British Library](http://bit.ly/britishlib_video) for students looking to conduct research projects using social media data 

## Project Tools 
To do this, I used a publicly available dataset containing Twitter data which you may download [here](https://catalog.docnow.io/) titled "Ireland 8th amendment referendum vote". Alternatively, the .txt file is also included in repository. I chose to use Python given its ease to work with and R/ R Studio's speed limitations in processing big data.  Feel free to access the full script [here](https://github.com/trisharjani/twitter_sentment_python/blob/master/Cleaning_Sentiment_News.ipynb). Kindly flagging that this code is quite long and may take a few tries to load.

Writing in Python 3.5, I used Jupyter Notebook and Anaconda. Below are some of the key packages I used for data exploration, manipulation, analysis and visualisation.   

* numpy 
* pandas 
* seaborn
* nltk (natural language toolkit)
* matplotlib
* statsmodels

Network analysis was performed using a different program, namely [CytoScape](https://cytoscape.org/). It could have alternatively been done using the NetworkX package in Python however since I was using my laptop, I was computationally limited and thus it was most accessible to use a different application which was also able to provide basic network measures such as degree centrality, betweenness centrality, eigenvector centrality etc. 

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

In order to identify whether the user posting the data has an impact on the retweet count and/or probability of a tweet being retweeted, each user needed to be characterised as either i) a campaigner from ‘yes’ camp, ii) campaigner from the ‘no’ camp, iii) a recognised news source, iv) a politician/ political party or, v) neither. To do this, a number of supplementary data sources were sought to generate a list to filter the usernames by. A similar filtering approach was adopted by Gross and Johnson (2016). Once this was done, dummy variables for each type of user were created. These were critical to the regression analysis presented later.

## Data Visualisations 

#### Heatmap of correlations to test multicollinearity:

<img src="https://github.com/trisharjani/twitter_sentment_python/blob/master/images/heatmap_correlations.jpg" width="400" height="300"/>

#### Average Sentiment of Tweets over Time: 

![alt text](https://github.com/trisharjani/python/blob/master/images/sentiment_over_time.jpg "Sentiment over Time")

#### Network Analysis (smaller cluster represents mostly no-endorsement tweets):
_Lines represent re-tweets, dots represent accounts_ 

[Click here for the zoomed version where node names are visible](https://github.com/trisharjani/twitter_sentment_python/blob/master/images/network%20mapping.jpg)

<img src="https://github.com/trisharjani/python/blob/master/images/network%20mapping.jpg" width="600" height="700"/>

#### Regression Analaysis (Please refer to the table above as a key for the 1,2,3,4):

<img src="https://github.com/trisharjani/twitter_sentment_python/blob/master/images/relational-plots.jpg" width="500" height="500"/>

## Summary of Conclusions 

The recent growth in the consumption of online information has led to a series of concerns about psychological biases which may, in tandem with social media tools that facilitate it, generate unprecedented levels of polarisation within society. In order to better understand the underlying motivation behind a given behaviour of sharing information which reinforces one’s view, this paper has correlated user-level features and content-level features impacts the reposting of a tweet. A key assumption being that a repost of a tweet can fairly be interpreted as an endorsement of its content.

* The results display some indication of emotional affect playing a part in determining how much a post is shared. In this context, tweets with a more negative sentiment appear to generate a significantly higher retweet count. 

* On a user-level, tweets posted by “official” sources including local Irish political parties, news sources (both local and international) and campaign accounts (both yes and no) display a consistently negative correlation with retweet count. These do not confirm the findings of some literature that demonstrates news tweets are more likely to be retweeted (Naveed et al., 2011). Neither do they confirm the fact that many of Twitter’s most followed accounts are news (Twittercounter, 2018) and the idea that Twitter is used as news medium (Kwak et al., 2010). It is unclear whether this finding is contextual or can be extrapolated to other contexts.

* This paper also demonstrates some homophily among campaign accounts and those directly retweeting campaign accounts; confirming previous literature that measures homophily in political contexts (Halberstam and Knight, 2016). Together, the deviation away from “official” information sources and the tendency to form “clusters” when sharing information demonstrates warranted concerns within literature claiming polarisation. 

### Bibliography #### 

Gross, J. H., & Johnson, K. T. (2016). Twitter Taunts and Tirades: Negative Campaigning in the Age of Trump. PS: Political Science & Politics, 49(04), 748–754. https://doi.org/10.1017/S1049096516001700

Halberstam, Y., & Knight, B. (2014). Homophily, Group Size, and the Diffusion of Political Information in Social Networks: Evidence from Twitter (No. w20681). Cambridge, MA: National Bureau of Economic Research. https://doi.org/10.3386/w20681

Hutto, C. ., & Gilbert, E. (2014). VADER: A Parsimonious Rule-based Model for Sentiment Analysis of Social Media Text. Eighth International Conference on Weblogs and Social Media. Retrieved from http://comp.social.gatech.edu/papers/icwsm14.vader. hutto.pdf.

Kwak, H., Lee, C., Park, H., & Moon, S. (2010). What is Twitter, a social network or a news media? In Proceedings of the 19th international conference on World wide web - WWW ’10 (p. 591). Raleigh, North Carolina, USA: ACM Press. https://doi.org/10.1145/1772690.1772751

Naveed, N., Gottron, T., Kunegis, J., & Alhadi, A. C. (2011). Bad news travel fast: a content-based analysis of interestingness on Twitter. In Proceedings of the 3rd International Web Science Conference on - WebSci ’11 (pp. 1–7). Koblenz, Germany: ACM Press. https://doi.org/10.1145/2527031.2527052

Twitter Counter. (n.d.). Twitter Counter. Retrieved from https://twittercounter.com/
