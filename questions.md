* Density estimation (using say, the kernel density estimator) can be used to perform classification.
  * True. Estimate the joint density P (Y , X ), then use it to calculate P (Y |X )

* PCA and Spectral Clustering (such as Andrew Ng’s) perform eigen- decomposition on two different matrices. However, the size of these two matrices are the same.
  * False

* For any two variables x and y having joint distribution p(x,y), we always have H[x, y] ≥ H[x] + H[y] where H is entropy function.
  * False

* The log-likelihood of the data will always increase through successive iterations of the expectation maximation algorithm.
  * False

* One disadvantage of Q-learning is that it can only be used when the
learner has prior knowledge of how its actions affect its environment.
  * False

* Both PCA and linear regression can be thought of as algorithms for minimizing a sum of squared errors. Explain which error is being minimized in each algorithm.
  * PCA re-construction error abd LR is residual error

* Difference between Maximum likelihood and maximum apriori
  * Maximum Likelihood finds the parameter which maximises the likelihood function
  * MAP maximises the posterior probability

* Similarity between Feature Selection and PCA
  * Both deal with curse of dimensionality. 

* Any MDP converges after the 1st value iteration for a discount factor γ = 0;
  * True, since all the converged values will be just immediate rewards.

* An MDP with N states and no stochastic actions (that is, each action has only one outcome) converges after N value iterations for any 0 ≤ γ < 1.
  * False. Consider a situation where there are no absorbing goal states.

* What is the effect on the means found by k-means of overlapping clusters
  * They are pushed further apart than the true means would be

* Suppose we have a large training set. Name a drawback when using a k Nearest Neighbor during testing.
  * k-NN is slow in testing phase, since the time complexity for finding k nearest neighbors is O(knd). n is number of training data points. d is number of dimensions.

* L2 loss is more robust to outliers than L1 loss.
  * False. The gradient of L2 loss can grow without bound whereas the L1 loss gradient is bounded, hence the influence of an outlier is limited.

* Why is feature selection required
  * To deal with curse of dimensionality 
  * Interoperability and insight

* Name 2 types of feature selection and how are they different
  * Filtering - Uses domain knowledge , Ignores learner bias, relationship and is fast
  * Wrapping - Slow, takes the bias of the learner, uses feature relationships. Can be sped up by Randomized optimization and forward and backward sequential selection
  
* What is feature transforation 
  * Finds a subsets of new features by linear combination of the features
  
* Difference between relevance and usefulness ?
  * Relevance measures the effect of a feature on Bayes optimal classifier
  * Usefullnes measures the effect of a feature on the error of a particular predictor
  
 *  What is a feature weakly relevant ?
  * When it is not strongly relevant
  * When there exists a subset of feature, S and adding to it improves BOC
 
 * How is PCA different from ICA
  * PCA looks for direction with maximum variance, ICA looks for maximum independence
  * PCA has all principal component mutually orthogonal, ICA finds maximum mutual information
  * PCA finds globally varying features, ICA finds locally



 
