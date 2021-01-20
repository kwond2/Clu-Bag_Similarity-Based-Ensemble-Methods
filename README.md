# Similarity-Based-Ensemble-Methods
(Recent TO DO: Clean up ipynb verbose output from keras models, organize/add markdown to each cell, clean + add other files)

This repo consists of the experimental results of the proposed Clu-bag ensemble method. The idea is to initially estimate a probability density function of the datset via some clustering or directly by density estimation, then assign a "clustering" or "peak" to a model (i.e. equivalent models), then use a modified form of bootstrap aggregation. First, we place higher probabilities on resampling data points closer to the mean of the assigned cluster. After training, we use the estimated posterior probability from our clustering/density estimation for each cluster as a convex combination of the corresponding model predictions, to come up with a weighted prediction. 
The intuition is that the procedure provides us with a more robust model from bagging, while also improving accuracy/reducing loss by reducing the "complexity" of the data - each model learns from "similar" data, which we hope learns the more subtle yet important differences between them, compared to learning patterns from a mix of data. A more formal analysis and deeper intuition can be found in the PDF [To be added].

The current implementation (for now) primarily uses a mixture of gaussians (GMM) to estimate the posterior probabilities (k-means + EM). However, it can be found in the literature to estimate a density from a clustering such as k-means, without resorting to more explicit density estimation approaches [To be added]. Also, because of the various testing that needs to be done, various APIs are used to improve training and implementation speed.

## What has been implemented so far?

#### 1. Fashion MNIST Multiclass Classification
  - LeNet5 (CNN), comparing Clusterbag method with GMM (k-means + EM) Density Estimation, with standard LeNet5, and bagged LeNet5.

## What needs to be implemented?

A LOT needs to be done. What I've put so far is only a few minor experiments (which have demonstrated a decrease in accuracy compared to the raw model and bagged model! Statistically unsignificant.)

Explicitly put:
#### 1. Formal/rigorous underpinnings of the guarantees the method provides, and identifying what would theoretically work.
  - How does the "quality" of the clusterings affect the theoretical accuracy? 
    - How does the number of clusterings affect the theoretical accuracy?
  - Can we formally prove for a simple case that that the procedure in expectation reduces/bounds the variance/overfitting? Significantly? Under what circumstances?
    - Is the overhead of a clustering algorithm "worth it"?
  - Implementing on other clustering methods - does this just become a hierarchical clustering model? 
    - Although more out of scope, can generalizing models to be hierarchical improve performance? (I.e., hierarchical neural networks, but doesn't that just imply 1 large NN?)
#### 2. Empirical results of (1.)
  - Varying the quality of clusterings
    - by implementing other clustering/density estimation methods, such as X-means, cross validated k-means, other density estimation approaches
    - similarly, varying the number of clusters
#### 3. Implementation of of other models
  - Kernel methods, SVM
  - "Simpler" Models
#### 4. Model accuracy significance testing
