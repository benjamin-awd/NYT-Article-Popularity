# Capstone Project: Predicting the Popularity of New York Times Articles

## Introduction
The New York Times is one of the most popular news platforms in the world and is visited by a countless number of visitors each day.

The New York Times' focus on subscribers sets them apart in crucial ways from other media organizations. Instead of trying to maximize clicks and sell low-margin advertising, the Times believes in providing high quality journalism and building up reader loyalty through community engagement.

In 2020 alone, there were nearly 5,000,000 comments posted on New York Times articles. That's 13,000 comments per day. While the Times has adopted [machine learning](https://www.nytimes.com/2017/06/13/insider/have-a-comment-leave-a-comment.html) to improve the comment moderation process, a large part of the moderation is still done [by hand](https://www.nytimes.com/2017/09/27/reader-center/comments-moderation.html). In short, the New York Times <b>can't allow comments on every article</b> due to manpower restraints.

This is the problem my project aims to resolve. Having the probability of whether an article is popular or unpopular can help improve the allocation of moderation resources. This will <b>improve comment moderation efficiency</b>, and potentially lead to a larger number of articles being opened for comments.

This could also allow the Times staff to make tweaks to increase article popularity before publishing an article, if they so desire.

This project therefore aims to answer:
- How can the NYT staff improve article popularity?
- Can we accurately predict article popularity? What are the most important predictors?

## Executive Summary

For this project, I scraped over 16,000 articles and 5,000,000 comments using the [nyt-scraper](https://github.com/ietz/nytimes-scraper) package. Some basic data cleaning and pre-processing was also done.

The top-performing model was a XGBoost Classifier which achieved an ROC-AUC score of <b>0.869</b> and an accuracy of <b>0.786</b>. A wide range of feature engineering techniques were used to accomplish this, including sentiment analysis and transformation of categorical features to ordinal features based on overall average popularity. 

Generally, I found that an article's <b>news desk, section, and subsection had a heavy influence </b> on whether it was popular or not. Text-based features like overall word count, headline/abstract length also played a key role. Longer articles tended to be more popular, while having a shorter headline/abstract generally improved popularity. 

The sentiment of the headline/abstract also played affect popularity, where articles with a more negative headline/abstract did better than articles with a neutral headline/abstract. The hour of publication also had an effect on popularity, where articles published late at night tended to draw more comments.

<img src='./assets/popular_topics.png' content-align="center">


Additionally, certain topics tended to be naturally more popular. Around 80% of articles mentioning Donald Trump each month had more than 90 comments, while only 20% or 30% articles around Real Estate news drew more than 90 comments.


## Recommendations

For articles that our model predicts to be unpopular, the following can be done:
- Re-write ‘neutral’ headlines & abstracts
- Shorten length of headlines & abstracts and include a question mark
- Change publication time to between 10pm and 3am
- Make sure the story is tied to the current socio-political context and use the right keywords
- Use a recommendation system to drive traffic to from popular articles to unpopular articles

## Limitations

Of course, just because an article has a low number of comments doesn't necessarily mean it's a low-performing article. The article might not appeal to regular commentators, and might do better on social media.

The NYT has to also uphold a degree of journalistic integrity -- even though using a click-bait headline might get them more comments, it’s in their own interest to remain an impartial and trusted source of news.

Additionally, this model is heavily affected by an article's news desk / section / subsection. More work should be done to ensure that an article's popularity isn't over or under predicted. Other predictors that could be looked into include topic 'freshness', where topics that are new tend to do much better than old topics (unless it's about Donald Trump).

## Data Dictionary

The documentation for the NYT articles / comments APIs can be found [here](https://developer.nytimes.com/docs/articlesearch-product/1/overview) and [here](https://developer.nytimes.com/docs/community-api-product/1/overview).