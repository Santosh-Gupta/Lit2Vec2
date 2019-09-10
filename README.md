# Lit2Vec2

A book recommender for rare books, containing 2,829,853 books. 

## Inspiration

Most book recommenders tend to recommend more popular books, we wanted to create a recommender for rarer books. 

## Data

We were able to obtain anonymized book ratings for 3 million users. We filtered the ratings to only books that each user enjoyed, so only books containing scores of 4/5 and 5/5.

For those wanting to train on our data, here is a folder containing the training data

https://drive.google.com/open?id=1FePFPkGk_cx8KwJZOZ5D14vpTVnGyphf

The 'GoodReadsUser4MS.h5' file is the main training file, which contains the annoymized userID and the embeddingID in each datapoint. The rest of the files are dictionaries for converting the embeddingIDs to titles and authors. 

## Model architecture and training parameters

The training algorithm is based on the skip-gram version of word2vec. A 'target' book is a book chosen at random from the list of books a user has rated, and then the 'context' books are 4 other books, chosen at random from the same list, excluding the target book. We trained the embeddings for 10 epochs over our data. 

For the recommender to recommend more rare books, for the negative samples we chose to sample from a log-uniform distribution [https://stats.stackexchange.com/questions/155552/what-does-log-uniformly-distribution-mean] and we ordered the books with the most occuring books at the head of the distribution, and the least occuring books occuring at the tail of the distribution. What this means is that the frequency of a particular book being selected as a negative sample is correlated with how popular the book is. Which allows for increased embedding similairty properties for the more rare books. 

