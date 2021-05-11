### TOPIC : SIMILARITY AWARE DEEP ATTENTIVE MODEL FOR CLICKBAIT DETECTION

### (INVOLVES USING BI-DIRECTIONAL LSTM MODEL)

### AIM : To determine if a particular web-link is news or clickbait by examining its title and body(content) by determining the similarity between them.

### MODEL USED - Bi-Directional Long Short-Term Memory (LSTM)


### THEORY

Clickbait is a type of web content advertisements designed to entice readers into clicking accompanying links. Usually, such links will lead to articles that are either misleading or non-informative, making the detection of clickbait essential for our daily lives. 
- Little attention has been paid to the relationship between the misleading titles and the target content, which we found to be an important clue for enhancing clickbait detection.
- In this work, we propose a similarity-aware attentive model (Bi-Directional LSTM Model) to capture and represent such similarities with better expressiveness.

### MODEL DEFINITION
- The model represents local similarities as vectors to combine them with other features for the future prediction easily.
- We introduce the ways of either using only similarity information or combining the similarity with other features to detect clickbait. We further employ an attention-based bidirectional Long Short Term Memory(LSTM) model to obtain robust representations of textual inputs.
- We evaluate our framework on a dataset of clickbait challenge
- The experimental results demonstrate its effectiveness in detecting clickbait and its competitive performance against the baselines

### DATASET

**Clickbait Challenge** is a benchmark dataset for the clickbait detection
(https://www.kaggle.com/c/clickbait-news-detection/overview).

- The training , validation & testing dataset contains over 25000, 3550 & 5600 labelled pairs of posts respectively.
- The 3 columns of dataset are : id(1,2,3,4...), title(title of the web link), text(content of the web page linked to), label(clickbait or news).
- We assigned the label ‘news’ as 1 and ‘clickbait’ as 0.
- For testing of dataset : a lower score stands for the lower probability of a post being clickbait. Then we regard the post with the mean score under 0.5 as news, else clickbait.

### GOAL : Predict a label Y = {y 1 , y 2 ,... , y N } of these pairs, where y i = 0 if headline i is a clickbait.
Our framework includes three parts: learning latent representations, learning the similarities, and using the similarity for the further predictions.

##### EXPERIMENTATION STEPS

1. PRE-PROCESSING (LEARNING THE LATENT REPRESENTATION)

```
● Preprocess the dataset by removing the rows with empty heading and/or empty body.
● Then remove all the punctuation and stop words, make the sentence in a lower form, and did word lemmatization
● Convert these cleaned input (heading, body) to vectors using DOC2VEC.
```

2. THE MODEL (LEARNING THE SIMILARITY)

```
● An architecture with two parallel RNN model (BiDirectional LSTM Model) is created, each taking a different input (one taking heading vector as input, another taking body vector as input), whose output will be used for the future model.
● The final model is created using a Lambda layer, with the above 2 created architectures and a distance (a keras Tensor Object) computed using the cosine similarity between the 2 corresponding vectors of a web-link (title and body)
● This model is now trained for epochs = 100 , optimizer = Adam, loss = contrastive loss & early stopping algorithm (callbacks).
```

3. THE PREDICTIONS
```
● The model is now used to predict values for the testing dataset (which was also pre-processed).
● A lower score stands for the lower probability of a the pair (heading and title) of being a clickbait (due to cosine similarity between the two, more the similarity - more they are related and thus not a clickbait).
● So, we regarded the post with the mean score under 0.5 as news, otherwise as clickbait.
```

### RESULTS

The trained model gave the following results on validation data:

```
➔ ACCURACY : 78.81%
➔ PRECISION VALUE : 0.
➔ RECALL VALUE : 0.
➔ F1-SCORE : 0.
```
Similarly, we predicted values for data(testing dataset from the clickbait challenge).
