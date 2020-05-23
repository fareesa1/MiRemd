# Music Recommendation System with Deep Learning and Cosine Similarity
This is a *Content-Based* recommmendation systems focus on properities of items. Similarity of items is determined by measuring the similarity in their properties.
## Overview
Traditinally, *Collaborative filtering* is a common method for Recommendation systems. The idea of *collaborative filtering* is to determine the users’ preferences from historical usage data, focus on the relationship between users and items. But perhaps the biggest problem is that **new and unpopular items cannot be recommended:** if there is no usage data to analyze, the collaborative filtering approach breaks down. This is the so-called **cold-start problem**. 
<br> *Content-based recommendations* make it possible for us to recommend new released or unpopular songs to listeners. 
The basic idea is that I use the CNN network to train as a classifier with labels that are 8 different song genres on the Free Music Archive dataset. The trained network is then modified by discarding the softmax layer i.e. creating a new model which works as an encoder. This encoder takes as input slices of a spectrogram one at a time and outputs a 40 dimensional latent representation of that respective slice. This generates multiple latent vectors for one spectrogram depending on how many slices were generated. These multiple vectors are then averaged to get one latent representation for each spectrogram. 
<br> The *Cosine similarity* metric is used to generate a similarity score between one anchor song and the rest of the songs in the playlist set. The two songs with the highest similarity score with respect to the anchor song are then outputted as the recommendations.
<br> **The network architecture looks like this:**
![](https://i.imgur.com/cSQpKqe.png)
## Training model
### Process data
The dataset I use to train the network is fma_small file from the [Free Music Archive](https://github.com/mdeff/fma) consist of 8,000 tracks of 30s, 8 balanced genres ( Hip-Hop, International, Electronic, Folk, Experimental, Rock, Pop, and Instrumental)(GTZAN-like).
<br> The mel-frequency spectrogram of track in the dataset look like this:
![](https://i.imgur.com/OC4INnI.png)
<br> I will then slice into small images of 128x128 pixels in grayscale levels.
### Training
I'm using [Residual Block](https://arxiv.org/abs/1512.03385) into Convolutional neural network to increase the model's performance.
![](https://i.imgur.com/lx270ui.png)
<br> Tensorboard
![](https://i.imgur.com/NWR5CIQ.png)
<br> **Performace on test set**
```
Test Accuracy: 89.9450%
```
![](https://i.imgur.com/qi5IAd9.png)
