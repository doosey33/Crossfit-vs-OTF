## Project 3: Crossfit vs. Orange Theory

### Problem Statement

Crossfit and Orange Theory are two of the biggest fitness regimen studios in the country. Both boast huge followings in memberships and in online presence as well. While they both aim to get you in shape through exercise, their methods differ on how to achieve your fitness goals. Crossfit is known to have a bigger strength training component to its workouts, while Orange Theory emphasizes cardio more.
   
   As a data scientist, the purpose of this project is to use data from the respective subreddits of each gym to build a model that will be able to differentiate between the two when given a sample of text. From there, I am hoping to be able to make a prediciton on which group is happier/more satisfied with their workouts.


#### Datasets

Datasets were created by pulling a 1000 of the most recent posts from each subreddit, using the pushshift API, from the following url: https://api.pushshift.io/reddit/search/submission?subreddit=boardgames

The posts were then compiled into two separate dataframes, by respective subreddit.
- Crossfit ['crossfit.csv'](./datasets/crossfit.csv)  
- Orange Theory ['orangetheory.csv'](./datasets/orangetheory.csv)  


### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|author_fullname|object|gyms_df|combination of a thing's type (e.g. Link) and its unique ID which forms a compact encoding of a globally unique ID on reddit|  
|title|object|gyms_df|the title of the link|
|selftext|object|gyms_df|the raw text. this is the unformatted text which includes the raw markup characters such as ** for bold. <, >, and & are escaped. Empty if not present| 
|score|int|gyms_df|the net-score of the link. note: A submission's score is simply the number of upvotes minus the number of downvotes|
|subreddit|object|gyms_df|subreddit of thing excluding the /r/ prefix|
|sub_value|int|gyms_df|numerical representation of subreddit; 1:OrangeTheory, 0:Crossfit|
|title_tokens|object|gyms_df|tokenized chunks of title data in list form|
|selftext_tokens|object|gyms_df|tokenized chunks of selftext data in list form|
|title_length|int|gyms_df|total sum of each character in title data|
|selftext_length|int|gyms_df|total sum of each character in selftext data|
|title_word_count|int|gyms_df|total sum of each word in title data|
|selftext_word_count|int|gyms_df|total sum of each word in selftext data|


### Methodology

Using Natural Language Processing(NLP) tools, we take the text data from the post titles and selftext and structuring them into a form that the computer can understand as language. This was done by tokenizing, Lemmatizing, and Stemming to break each individual word into its simplest form. Then transforming this unstructured text data into an organized matrix of numbers that the computer can process, with the help of a Count Vectorizer. 


### Conclusions and Recommendations

My model did fairly well at predicting subreddits. The distribution of word counts and character length provided a good way to differntiate between the to subreddits. I would have liked to incorporate that into my model features to see if it would have improved the accuracy score. 

The gridsearch models, while they took a long time to run through numerous hyperparameters, did no better and at times even worse than the default pipeline models. I learned from this that more parameters don't necessarily mean better results.

Unfortunately, the Sentiment Analysis did not provide any significant data in determining which fitness community was happier with their workouts. The compound scores for the title and selftext of each subreddit's post were overwhelmingly low, and neutral. Going forward I think it would do better with a lot more data, and more in depth EDA to filter out a lot of unnecessary words that cloud the analyzer. An interesting aspect I did discover from the posts during cleaning and analysis was that, a good number of users from both communities tend to treat the message boards as personal ads. The contents of most of the posts were a bit racy, and I discovered as well during tokenizing and lemmatizing that a number of words were being split on the letters 'M' and 'F'. After further analysis, I discovered that the posts were punctuating these letters with brackets to denote 'Male' and 'Female'.

Although I was unable to answer which community was happier, I discovered a lot of little nuances during natural text EDA that will help me in future projects.



