# Literature - Predicting Personality Traits

## [Towards a Pyschographic User Model From Mobile Phone Usage](/predicting-personality/mobile-phone-usage.pdf)

#### Traits
50-item sample test from IPIP website with Cronbach's alpha, as reported by IPIP, of .79-.87. Cronbach's alpha for their users not reported. Only the primary big 5 traits are measured. There are 39 observations in this test.

#### Model
Features used are related to call usage and social network analysis of the users. Selected features were number of calls, duration of calls, and messages sent/recieved at different times of day, number of contacts, number of strong contacts. Used SVM Recursive Feature Elimination to select features followed by SVM regression w/ Gaussian kernel, cross validated with MSE.

#### Objective & Results
MSE of regression is compared to MSE of the mean for each trait. If we translate that to Pearson correlations they achieve scores between .55 and .66 across all 5 traits.


## [Measuring personality from Keyboard and mouse use](/predicting-personality/personality-from-keyboard-use.pdf)


#### Traits
IPI-NEO 120 question test with 30 trait/subtrait combinations. No report on consistency. 26 participants.

#### Model
Uses logs of users using computer programs in experimental setting, measures number of events and speed of events and frequency of switing windows etc.

#### Objective & Results
Pearson correlations between individual features and personality traits, reported traits were based on statistical significance of correlation. Linear regression was attempted to see if more variance can be explained as a linear combination of measured behavior, without much improvement. Reported correlations are between .4 and .6. No corrections made for multiple testing.


## [Towards customized user interfaces](/predicting-personality/personality-and-skin-color.pdf)

#### Traits
IPI-NEO 120 question test with 30 trait/subtrait combinations. No report on consistency. 16 participants.

#### Model
Looks at use of media players (WinAmp!), measuring two separate sets of traits, one being the way in which users interact with the app (frequency, speed), the second being the appearence/color the users choose for the app.

#### Objective & Results
It compares both of these traits with personality through simply examing spearman correlations and reporting statistical significant correlations. Significant correlations for actions are between .54 - .67 accross all traits, while for color of application they see correlations between .46-.73 for all traits except nueroticism. There's a .73 spearman correlation between choosing a black media player and Openness/imagination. No corrections made for multiple testing.


## [Automatic Recognition of Personality in Conversation](/predicting-personality/personality-in-conversation)

#### Traits
5-7 independent observers scored the text extracts (more detail is not given), but they report inter-observer reliability via correlation and significance of that correlation for all dimensions with (r = 0.84, p < 0.01). 96 participants.

#### Model
Features created via several closed-vocabulary NLP processes: LIWC, MRC, Prosodic features (pix, intervals, etc), and "Utterances" (ratio of comamnds/prompts/questions/assertsion). In other words, linguistic features that have been manually chosen by experts for the language. They used RankBoost to train model (created by the AdaBoost folk). Not specified but looks like the underlying models are trees.  They show how different groups of features, vs aggregations of all, perform differently in predicting different traits, although it's unclear to me why restricted subsets in a boosting context should perform better, they seem to.

#### Objective & Results
Start initially by stating that "we formulate personality recognition as a ranking problem". Error reported is "ranking error", which seems to be standard to RankBoost. In their results the rank error ranges from .26 - .39, which they claim shows that "personality can be recognized". I do not have an understanding of what RankError is and recommend reading the RankBoost paper to understand. 


## [25 Tweets to Know You](/predicting-personality/25-tweets.pdf)

This is the main article behind IBM's Personality Insights.

#### Traits
50-question IPIP administered via a custom web app. Means of each score are reported (middle-ish), but not consistency. 1300 users with 200 tweets each.

#### Model
Features created by first creating a word embedding over corpus of tweets, then creating a document vector for each tweet as an average of the word vectors in a tweet. Gaussian process regression using these document vectors for the tweets of a user is used as model and compared with Ridge Regression ontop of 3-gram bag of words (previous state of the art, which is presented in "Personality, gender, and age in the language of social media"), as well as Ridge Regression on top of closed-vocabulary LIWC features. 

#### Objective & Results
Objective function is cross validated Pearson Correlation, in which their method is shown to be ~33% better with correlations from .29 - .42. To compute statistical significance they perform an ANOVA test on average absolute error across all traits for the three compared methods and show that theirs is significantly better.


## [Personality, Gender, and Age in the Language of Social Media](/predicting-personality/personality-gender-and-age.pdf)

Very linguistic and focuses a lot on inference. 

#### Traits
A variety of NEO-PI-R with 20-100 questions. They report retest reliability of Cronbach's alpha > 0.80, but its not clear if that's the official score of the test or their own data. 75000 users.

#### Models
They build a ridge regression model that includes LIWC features as well as LDA topic modelling and 3-gram bag of words, the latter two they show to perform better than the LIWC features, explaining that vocabulary methods learned from data seem to perform better than clsoed-vocabulary methods, despite the nice interpretability of the latter. 

They also specify very clearly their goal being interpretation by finding all features (words) that are predictive of a trait, including collinear features, which they differentiate from past work. This is an important example for us as similarly the interpretability per-trait is most likely more valuable than multi-response prediction of all traits.

#### Objective & Results
They mention that they, as in some past literature, also treat the personality trait prediction as a classification problem, classifying high/low traits and ignoring the middle, but defend the use of Pearson correlation as a more natural objective function as personality is measured on a continuous scale.

Most importantly, when reporting their correlations they mention that their best score, 0.42, "fell just above the standard 'correlational upper-limit' for behavior to predict personality (0.3 - 0.4)", which they give Pyschological Testing and The Power of Personality as references for this number.


## Private Traits are Predictable from Digital Records of Human Behavior(/predicting-personality/private-traits.pdf)

#### Traits
20-question IPIP questionnaire for 5 traits. 58000 participants.

#### Model
The features were the Facebook likes and demographic profiles of all participants. A sparse binary array of likes across all pages was created for each user, then PCA ran to reduce to 100 components, and linear regression ran on personality traits.

#### Objective & Results
Pearson correlation was reported. This report, for all the Big Five traits, compared their correlation with the retest correlation for each feature, but does not report where they got the retest correlation numbers. They report correlations between 0.29 - 0.43, where the "baseline" retest correlations are reported between 0.55 - 0.75. The best predictor was for Openness, which was 0.43 for their prediction and 0.55 for re-test reliability.


# Literature - Relevant Psychology Background

## Validity of Personality Tests

Personality traits are a latent feature. Even the most "direct" measures available to us (questionaires), are far from perfect measures of the personality traits. Very little of the literature above, the majority of which comes from the computer science world, attempts to formally address the validity of the personality questionnaires. This validity has been well-studied, considered, and questioned in the Psychology literature, however, and is worth considering. 

## [Internal Consistency, Retest Reliability, and their Implications For Personality Scale Validity](/predicting-personality/personality-scale-validity.pdf)

There are two major factors in validity that are most often reported. They are related, but not identical:

#### Cronbach's alpha
This is a measure of "internal consistency." The word "internal" in this context refers to the questions within a given trait. For example, if a questionnaire consists of 65 questions, 13 for each of the 5 traits, Cronbach's alpha measures the variance within the 13 questions as compared to the variance in the trait itself. The higher the correlation among the 13 questions that measure a single trait, the higher the "internal consistency", and the higher the Cronbach's alpha. 

Naturally, there is a flip side to this. If the same question is simply repeated 13 times verbatim, the internal consistency will be perfect, but that will reduce the accuracy of the test for two reasons: 1) it will only measure one "aspect" of the trait and 2) the variance will be high, with small changes in the wording of that one repeated question, the score will vary wildly. For this reason, internal consistency is far from a full measure of validity.

#### Test-Retest Reliability
Take a group of participants, test them once, wait a month, test them again. The simple Pearson correlation between a each participants score on each trait across the two different time periods will be a measure of the test-retest reliability of that trait in that test. 

Test-retest reliability is much less often reported, simply because it is much more difficult to test subjects twice! Naturally this is also not a full measure of validity: the questions can be relatively irrelevant for the traits, which, if heterogeneously so, will show up in measures of internal consistency, but the same questions might perform very well in test-retest reliability if they are simple questions. 

Similarly it is important to distinguish between stability and retest reliability. Stability refers to the stability of traits within the person over time, and when tests are re-administered after long periods of time, differences in their scores might not only be a product of retest reliability error, but also a product of changes to the true underlying personality trait over time!

#### Numbers

Some numbers from this meta-analysis report alpha's between .58 - .9, and retest consistency between .66 and .92 for a 6-month period for the NEO-PI-R personality inventory.

## [Psychological Testing and Psychological Assessment](/predicting-personality/psychological-testing-and-assessment.pdf)

Self reports and reports of others/professionals/adults(vs. kids) can have correlations that are super low, .2-.3. Makes strong recommendations for always doing multiple tests for psychological testing. It can be seen that in predicting anything, personality traits never achieve correlation scores very high.

## [The Power of Personality]

Metaanalysis of research linking personality traits to life outcomes, spends a decent amount of time saying that personal psychology shouldn't be dismissed because of low coefficients, which range up to 0.4 for predicting behaviors or outcomes.


## [Revealing Dimensions of Thinking in Open-Ended Self- Descriptions](/predicting-personality/open-ended-self-descriptions.pdf)

Finds 7 factors in self-descriptions not fully correlated with big 5?? Still need to read. 


# Conclusions

* Cronbach's alpha is between .68 and .75 for our bigfive survey / traits. We can also look at variance within each individual user.

* RankBoost. ?
* Psychology papers on "correlational upper-limit" for behavior to predict personality...

# To Read
