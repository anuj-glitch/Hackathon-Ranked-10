# Analytics Vidhya Janatahack: Recommendation system

### Ranked 10 out of 12,010 registered users in the Recommendation system Hackathon organized in Analytics Vidhya.



![](https://github.com/anuj-glitch/Recommendation-system-Hackathon-Ranked-10/blob/master/submission.PNG)


## Problem Statement
 - Your client is a fast-growing mobile platform, for hosting coding challenges. They have a unique business model, where they crowdsource problems from various creators(authors). These authors create the problem and release it on the client's platform. The users then select the challenges they want to solve. The authors make money based on the level of difficulty of their problems and how many users take up their challenge.
 - The client, on the other hand makes money when the users can find challenges of their interest and continue to stay on the platform. Till date, the client has relied on its domain expertise, user interface and experience with user behaviour to suggest the problems a user might be interested in. You have now been appointed as the data scientist who needs to come up with the algorithm to keep the users engaged on the platform.

## What to recommend
 - The client has provided you with history of last 10 challenges the user has solved, and you need to predict which might be the next 3 challenges the user might be interested to solve. Apply your data science skills to help the client make a big mark in their user engagements/revenue.

## Data Description
for data desciption, there are three files:

 - train.csv: It contains the set of 13 challenges that were attempted by the same user in a sequence.
 - challenge_data.csv: Contains attributes related to each challenge
 - test.csv: Contains the first 10 challenges solved by a new user set (not in train) in the test set. We need to predict
 
![](https://github.com/anuj-glitch/Recommendation-system-Hackathon-Ranked-10/blob/master/data_desc.PNG)

## Evaluation Metric
 - The evaluation metric is Mean Average Precision (MAP) at K (K = 3). MAP is a well-known metric used to evaluate ranked retrieval results. E.g. Let’s say for a given user, we recommended 3 challenges and only 1st and 3rd challenges are correct. So, the result would look like — 1, 0, 1

 - In this case, The precision at 1 will be: 11/1 = 1 The precision at 2 will be: 01/2 The precision at 3 will be: 1*2/3 = 0.67 Average Precision will be: (1 + 0 + 0.67)/3 = 0.556.

## Solution:
- Approached as a Text Generation Problem; where a sequence of words is used to predict the next word
- Each user in the training set was replicated 3 times, i.e. sequence of the 10 challenges solved and their three labels (for 11th, 12th and 13th challenges).
- All the challenges were label encoded
- Now we had a multiclassification problem with 5606 classes and around 200k observations
- The classification is done using BiDirectional LSTM. This model was optimised (size of embedding was tuned)
- Further we tried using BiDirectional GRU. Here as well, embedding sizes were tuned.
- Finally we ensembled 6 models (3 LSTM with different embedding size & 3 GRU with different embedding sizes)
- During test time, we obtained a probability distribution for each sequence. Then, chose top-3 argmax probabilities as 11th, 12th and 13th challenges predicted.

