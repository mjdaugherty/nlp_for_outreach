# Conducting Better Public Outreach Using Natural Language Processing
Michael Daugherty\
31 January 2020\
DSI-10 DC\
Instructors: Adi Bronshtein and Chuck Dye

## Problem Statement & Objective:
The Northern Virginia Astronomy Club (NOVAC) has invited me to give a presentation on effective public outreach at its January meeting. In preparation for this talk, I intend to use computational analysis of many posts relating to astronomy made by laypeople on two boards on Reddit, r/space and r/Astronomy, to find and put into words those things that compel us to look up at the night sky so that we can better communicate them to interested members of the public.

## Original Sources of Included Data
[Astronomy subreddit](https://www.reddit.com/r/Astronomy)\
[Space subreddit](https://www.reddit.com/r/space)

## Internal Directory
The [code](code) directory contains Jupyter notebooks devoted to collecting, cleaning and modeling of the data.\
The [data](data) directory contains the data themselves.\
The [presentation](presentation) directory contains a .pdf of the slides presented at the monthly meeting of the [Northern Virginia Astronomy Club (NOVAC)](https://www.novac.com/wp/).

## Procedure and Methods
- Imported the numpy, pandas and requests libraries along with other necessary modules
- Used requests along with the [Pushshift Reddit API](https://api.pushshift.io/reddit/search/) to collect 10,000 comments (not submissions) from both subreddits
- Extracted the text of each post and the subreddit on which it was made and converted these into a pandas DataFrame
- Cleaned data by discarding duplicate posts and posts which had been deleted or removed and contained no useful text
- Combined posts into a single large DataFrame and exported to a .csv file
- Calculated a baseline score (minimum accuracy score for a useful model)
- Created a feature matrix and target vector of posts and binarized subreddit values, respectively
- Created a pipeline consisting of TFIDV vectorizer with a range of parameters and a multinomial Bayes classifier to vectorize and fit a model to the post data, respectively
- Obtained and compared accuracy scores from the model on the training and testing data
- Used GridSearch to try several different logistic regression models and select the best one
- Created a random forest classifier and fit it to the training data and extracted the most important features (words) for qualitative analysis

## Findings, Conclusions, Recommendations
- The multinomial Bayes and logistic regression models had very similar performance
- The accuracy score was similar for the training and testing data for both models, meaning that they were not overfit to the training data and we can expect the same accuracy on unseen data
- The random forest classifier was overfit even after limiting the depth to a maximum of 40 using GridSearch; its accuracy on the training data was much higher than the other two models but it was very slightly worse (though not terrible) on the test set
- Strictly for the purposes of classifying posts from two subreddits, either of the first two models or perhaps a different type such as a support vector machine would be best because of their higher accuracy and ability to generalize to new data; however, to solve the problem of this project, the random tree classifier is the most powerful because of the ability to grab the most predictive words from both subreddits\
- Future steps: try different types of models and techniques like tokenizing with regular expressions to try to improve accuracy

Interesting/useful words from random forest feature importances:
- amazing
- beautiful
- god
- earth
- humans
- Greek

## Executive Summary
One of the most important functions of amateur astronomy societies ("astronomy clubs") is to reach out to members of the public who may not be as familiar with the science and hobby of astronomy as we are. One of the biggest reasons to conduct public events is to inspire people of all ages and backgrounds to learn about the sciences and gain a broader perspective on human life and our place in the universe. There are many ways to do this, but all of them involve sharing those aspects of astronomy that appeal to people on a deep level.

A short list of the words which were highly important in classifying posts between the r/space and r/Astronomy subreddits is given in the previous section. These words suggest that people are drawn to astronomy for many reasons: amazement and awe, appreciation of beauty, spirituality, connection to nature, love of myths and stories. I believe that in order to foster curiosity and interest in the sciences (especially among young people), amateur and professional astronomers alike should highlight these aspects of astronomy and space science when engaging with those who may never have been exposed to the field. Although the enjoyment of nature and storytelling are by no means exclusive to astronomy, setting up a telescope in a public space provides us a unique opportunity to give others a look into the universe and get them thinking about the world outside our home planet. It is up to us to help make this an unforgettable experience.

My suggestion is simple: NOVAC members should spend as much time as possible sharing our telescope time with non-members. For every minute we spend with a telescope in our back yards, we should spend a minute with a telescope in a public park or on a university campus. Conducting more events like star parties and planetarium talks may be infeasible due to cost and limited range of venues, but as individuals we have the flexibility to reach many people and improve our communities.
