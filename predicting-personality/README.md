

# Literature - Predicting Personality Traits

## [Towards a Pyschographic User Model From Mobile Phone Usage](/predicting-personality/mobile-phone-usage.pdf)

From the literature review here we get two other papers included below, _Measuring personality from keyboard and mouse use_, _Towards customized user interfaces_, and _Automatic Recognition of Personality in Conversation_. 

SVM Recursive Feature Elimination to select features followed by SVM regression w/ Gaussian kernel, cross validated with MSE. Features used are related to call usage and social network analysis of the users. Selected features were number of calls, duration of calls, and messages sent/recieved at different times of day, number of contacts, number of strong contacts.

MSE of regression is compared to MSE of the mean for each trait. They claim the results are satissfactory, although it's unclear what makes them so. All target traits have a MSE improvement of less than 50% over the mean.

Only the primary big 5 traits are predicted, with 39 observations.


## [Measuring personality from Keyboard and mouse use](/predicting-personality/personality-from-keyboard-use.pdf)

Uses logs of users using computer programs in experimental setting, measures number of events and speed of events and frequency of switing windows etc. Statistical work consists of reporting Pearson correlations between these counts and personality traits, statistical significance is reported but it's not clear how that significance was measured (Gaussian assumption and Chi^2?). Reported correlations are between .4 and .6. 

They had 26 participants and the correlations are between 30 trait/subtrait combinations in the IPIP-NEO (5 traits, 6 subtraits per trait). 

Linear regression was attempted to see if more variance can be explained as a linear combination of measured behavior, without much improvement.


## [Towards customized user interfaces](/predicting-personality/personality-and-skin-color.pdf)

Looks at use of media players (WinAmp!), measuring two separate sets of traits, one being the way in which users interact with the app (frequency, speed), the second being the appearence/color the users choose for the app. It compares both of these traits with personality through simply examing spearman correlations and reporting statistical significant correlations. Significant correlations for actions are between .54 - .67 accross all traits, while for color of application they see correlations between .46-.73 for all traits except nueroticism. There's a .73 spearman correlation between choosing a black media player and Openness/imagination. 

Also all of the correlations are calculated on the 30 trait/subtrait pairs of the IPIP-NEO, and they had a total of 16 participants.

## [Automatic Recognition of Personality in Conversation]()

Start initially by stating that "we formulate personality recognition as a ranking problem". 

Features created via several NLP processes: LIWC, MRC, Prosodic features (pix, intervals, etc), and "Utterances" (ratio of comamnds/prompts/questions/assertsion). RankBoost to train model (created by the AdaBoost folk). Not specified but looks like the underlying models are trees. Error reported is "ranking error", which is 0.5 on a random baseline, and ranges from .26 - .39, which they claim shows that "personality can be recognized". They show how different groups of features, vs aggregations of all, perform differently in predicting different traits, although it's unclear to me why restricted subsets in a boosting context should perform better, that wasn't addressed. 

## [25 Tweets to Know You](/predicting-personality/25-tweets.pdf)

This is the main article behind IBM's Personality Insights. 

Creates features by creating a word embedding over corpus of tweets, then creating a document vector for each tweet as an average of the word vectors in a tweet. 

Gaussian process regression using these document vectors for the tweets of a user is used as model and compared with Ridge Regression ontop of 3-gram bag of words (previous state of the art, which is presented in "Personality, gender, and age in the language of social media"), as well as Ridge Regression on top of LIWC features. Objective function is cross validated Pearson Correlation, in which their method is shown to be ~33% better with correlations from .29 - .42. To compute statistical significance they perform an ANOVA test on average absolute error across all traits for the three compared methods. 

1300 users with 200 tweets each.

## [Personality, Gender, and Age in the Language of Social Media](/predicting-personality/personality-gender-and-age.pdf)

This gives a great introduction to LIWC feature creation. 

75000 users. 


## [Revealing Dimensions of Thinking in Open-Ended Self- Descriptions](/predicting-personality/open-ended-self-descriptions.pdf)

Finds 7 factors in self-descriptions not fully correlated with big 5?? Need to read!

## [Dark Triad](/dark-triad.pdf)


# TODO

* Cronbach's alpha? Consistency/Accuracy of our Ground Truth. 
* RankBoost. ? 
