# Lit2Vec2

A book recommender for rare books, containing 2,829,853 books. This project is a sequel to the original lit2vec project, which only contains 10,000 books. https://github.com/Santosh-Gupta/Lit2Vec

## Inspiration

Most book recommenders tend to recommend more popular books, we wanted to create a recommender for rarer books. 

## Data

We were able to obtain anonymized book ratings for 3 million users. We filtered the ratings to only books that each user enjoyed, so only books containing scores of 4/5 and 5/5.

For those wanting to train on our data, here is a folder containing the training data

https://drive.google.com/open?id=1FePFPkGk_cx8KwJZOZ5D14vpTVnGyphf

The 'GoodReadsUser4MS.h5' file is the main training file, which contains the annoymized userID and the embeddingID in each datapoint. The rest of the files are dictionaries for converting the embeddingIDs to titles and authors. 

To see how the data was used in training, please see our training notebook 'Lit2Vec2TrainingPublic.ipynb'

## Model architecture and training parameters

The training algorithm is based on the skip-gram version of word2vec. A 'target' book is a book chosen at random from the list of books a user has rated, and then the 'context' books are 4 other books, chosen at random from the same list, excluding the target book. We trained the embeddings for 10 epochs over our data. 

For the recommender to recommend more rare books, for the negative samples we chose to sample from a log-uniform distribution [https://stats.stackexchange.com/questions/155552/what-does-log-uniformly-distribution-mean] and we ordered the books with the most occuring books at the head of the distribution, and the least occuring books occuring at the tail of the distribution. What this means is that the frequency of a particular book being selected as a negative sample is correlated with how popular the book is. Which allows for increased embedding similairty properties for the more rare books. 

To fit all of the embeddings within the memory limits of our systems, we used SpeedTorch, a library designed to augment the training parameters of embeddings training. 

https://github.com/Santosh-Gupta/SpeedTorch

To see how exactly it was trained, please see our notebook

'Lit2Vec2TrainingPublic.ipynb'

## Azure Training Process

Due to the large size of the dataset and the resources required to train the Machine Learning model, we opted to use the Azure Machine Learning Workspace for the training cycle of our project. Azure gave us the facility of using Jupyter notebooks and Python scripts on their Virtual Machines to run numerous experiments in a straightforward environment.

As we had been using PyTorch in the initial prototypes of this project and in previous versions of this project, we found it best to use the PyTorch class within the Azure ML library. This lead to much cleaner setup of the experiments and their environments.

The intial step in this Azure experiment notebook is to define the workspace and the experiment variables. The compute target is then set up. This step allocates the resourcse that will be needed to run the experiments. In our case, we used the Standard_N6 and set a maximum of 4 nodes in the cluster.

We then set up the PyTorch object which allows us to use the training scripts that had been in use until now. Once set up with the appropriate command arguments and dependencies, we can pass this object as an argument to the Experiment object and submit the experiment to let it run. When the experiment completes, we register the model with the workspace where it will save along with a number of files being saved from within the training script. 

To see the Azure Experiment process, please see out notebook

'pytorch-train-l2v2.ipynb'
